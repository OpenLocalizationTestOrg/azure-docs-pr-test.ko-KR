---
title: "어떻게 tooconfigure (피어 링)에 대 한 라우팅 ExpressRoute 회로: 리소스 관리자: PowerShell: Azure | Microsoft Docs"
description: "이 문서를 만들고 hello private, public 및 Microsoft 피어 링 express 경로 회로 프로 비전에 대 한 hello 단계를 안내 합니다. 또한이 문서를 보면 toocheck hello 상태 업데이트 또는 회로 대 한 피어 링 삭제 방법을 알 수 있습니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a>PowerShell을 사용하여 ExpressRoute 회로의 피어링 만들기 및 수정

이 문서를 사용 하 여 만들고 hello PowerShell을 사용 하는 리소스 관리자 배포 모델에서 ExpressRoute 회로 대 한 라우팅 구성을 관리할 수 있습니다. Hello 상태, 업데이트 또는 삭제를 확인 하 고 피어 링 express 경로 회로 대 한 프로 비전을 해제할 수도 있습니다. 다른 방법 toowork toouse 회로 사용 하려는 경우 hello 다음 목록에서에서 아티클을 선택 합니다.

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

* Hello 최신 버전의 hello Azure 리소스 관리자 PowerShell cmdlet 필요 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. 
* Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md) 페이지 hello [라우팅 요구 사항](expressroute-routing.md) 페이지 및 hello [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에 페이지입니다.
* 활성화된 Express 경로 회로가 있어야 합니다. 너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다. hello ExpressRoute 회로이 문서의 toobe 수 toorun hello cmdlet을 가능 하 고 프로 비전 된 상태에 있어야 합니다.

이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다. 관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.

> [!IMPORTANT]
> 에서는 현재 보급 되지 않고 피어 링 hello 서비스 관리 포털을 통해 서비스 공급자가 구성 합니다. 이 기능을 곧 사용할 수 있도록 개발 중입니다. BGP 피어링을 구성하기 전에 서비스 공급자에게 확인하세요.
> 
> 

ExpressRoute 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다.(개인, Azure 공용 Azure 및 Microsoft) 선택한 순서로 피어링을 구성할 수 있습니다. 그러나 한 번에 하나씩 피어 링의 hello 구성을 완료 되었는지 확인 해야 합니다. 

## <a name="azure-private-peering"></a>Azure 개인 피어링

이 섹션을 사용 하면 만들기, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 개인 피어 링 구성을 Azure 있습니다.

### <a name="toocreate-azure-private-peering"></a>Azure 개인 피어 링 toocreate

1. ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.

  Hello 최신에서 PowerShell 설치 관리자를 설치 해야 [PowerShell 갤러리](http://www.powershellgallery.com/) hello Azure 리소스 관리자 모듈 hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 가져옵니다. 관리자 권한으로 PowerShell toorun이 필요 합니다.

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  모든 의미 체계의 버전 범위 알려진 hello 내의 hello AzureRM.* 모듈만 가져옵니다.

  ```powershell
  Import-AzureRM
  ```

  클릭할 수도 hello 알려진 의미 체계의 버전 범위 내의 select 모듈을 가져올 수 있습니다.

  ```powershell
  Import-Module AzureRM.Network 
  ```

  Tooyour 계정에 로그인 합니다.

  ```powershell
  Login-AzureRmAccount
  ```

  ExpressRoute 회로 toocreate hello 구독을 선택 합니다.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Express 경로 회로를 만듭니다.

  Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-arm.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.

  관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다. 이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다. 그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.
3. Hello ExpressRoute 회로 toomake 프로 비전 되 고도 사용 하도록 설정 되었는지 확인 합니다. 다음 예제는 hello를 사용 합니다.

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  hello 응답은 다음 예제와 비슷한 toohello입니다.

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Azure 개인 피어 링 hello 회로 대 한 구성 합니다. Hello 다음 단계를 진행 하기 전에 다음 항목 hello 했는지 확인 합니다.

  * / 30 서브넷 hello 기본 링크에 대 한 합니다. hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.
  * / 30 서브넷 hello 보조 링크에 대 한 합니다. hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.
  * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
  * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다. 이 피어링에 개인 AS 숫자를 사용할 수 있습니다. 65515를 사용하지 않는지 확인합니다.
  * **선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.

  다음 예에서는 tooconfigure 회로 대 한 피어 링 개인 Azure hello를 사용 합니다.

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Toouse MD5 해시를 선택 하면 다음 예제는 hello를 사용 합니다.

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > 고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.
  > 
  >

### <a name="tooview-azure-private-peering-details"></a>세부 정보를 피어 링 개인 Azure tooview

다음 예제는 hello를 사용 하 여 구성 세부 정보를 얻을 수 있습니다.

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure 개인 피어 링 구성

다음 예제는 hello를 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다. 이 예제에서는 100 too500에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a>Azure 개인 피어 링 toodelete

다음 예제는 hello를 실행 하 여 피어 링 구성을 제거할 수 있습니다.

> [!WARNING]
> 모든 가상 네트워크 없는지 hello ExpressRoute 회로에서 연결 된이 예제를 실행 하기 전에 확인 해야 합니다. 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a>Azure 공용 피어링

이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Azure 공용 피어 링 구성이 있습니다.

### <a name="toocreate-azure-public-peering"></a>Azure 공용 피어 링 toocreate

1. ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.

  Hello 최신에서 PowerShell 설치 관리자를 설치 해야 [PowerShell 갤러리](http://www.powershellgallery.com/) hello Azure 리소스 관리자 모듈 hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 가져옵니다. 관리자 권한으로 PowerShell toorun이 필요 합니다.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  모든 의미 체계의 버전 범위 알려진 hello 내의 hello AzureRM.* 모듈만 가져옵니다.

  ```powershell
  Import-AzureRM
  ```

  클릭할 수도 hello 알려진 의미 체계의 버전 범위 내의 select 모듈을 가져올 수 있습니다.

  ```powershell
  Import-Module AzureRM.Network
```

  Tooyour 계정에 로그인 합니다.

  ```powershell
  Login-AzureRmAccount
  ```

  ExpressRoute 회로 toocreate hello 구독을 선택 합니다.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Express 경로 회로를 만듭니다.

  Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-arm.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.

  관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다. 이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다. 그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.
3. Hello ExpressRoute 회로 tooensure 프로 비전 되며 사용 하도록 설정도 확인 합니다. 다음 예제는 hello를 사용 합니다.

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  hello 응답은 다음 예제와 비슷한 toohello입니다.

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Azure 공용 피어 링 hello 회로 대 한 구성 합니다. 다음 정보를 계속 진행 하기 전에 hello 했는지 확인 합니다.

  * / 30 서브넷 hello 기본 링크에 대 한 합니다. 유효한 공용 IPv4 접두사여야 합니다.
  * / 30 서브넷 hello 보조 링크에 대 한 합니다. 유효한 공용 IPv4 접두사여야 합니다.
  * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
  * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.
  * **선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.

  다음 예에서는 tooconfigure 회로 대 한 피어 링 공용 Azure hello를 실행 합니다.

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Toouse MD5 해시를 선택 하면 다음 예제는 hello를 사용 합니다.

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > 고객 ASN이 아닌 피어링 ASN로 AS 번호를 지정했는지 확인합니다.
  > 
  >

### <a name="tooview-azure-public-peering-details"></a>세부 정보를 피어 링 공용 Azure tooview

Cmdlet을 다음 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure 공용 피어 링 구성

다음 예제는 hello를 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다. 이 예제에서는 200 too600에서 hello hello 회로의 VLAN ID를 업데이트 중입니다.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a>Azure 공용 피어 링 toodelete

다음 예제는 hello를 실행 하 여 피어 링 구성을 제거할 수 있습니다.

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a>Microsoft 피어링

이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Microsoft 피어 링 구성이 있습니다.

> [!IMPORTANT]
> 이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 hello Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다. Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다. 자세한 내용은 [Microsoft 피어링에 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft 피어 링

1. ExpressRoute에 대 한 hello PowerShell 모듈을 가져옵니다.

  Hello 최신에서 PowerShell 설치 관리자를 설치 해야 [PowerShell 갤러리](http://www.powershellgallery.com/) hello Azure 리소스 관리자 모듈 hello ExpressRoute cmdlet을 사용 하 여 순서 toostart에 hello PowerShell 세션으로 가져옵니다. 관리자 권한으로 PowerShell toorun이 필요 합니다.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  모든 의미 체계의 버전 범위 알려진 hello 내의 hello AzureRM.* 모듈만 가져옵니다.

  ```powershell
  Import-AzureRM
  ```

  클릭할 수도 hello 알려진 의미 체계의 버전 범위 내의 select 모듈을 가져올 수 있습니다.

  ```powershell
  Import-Module AzureRM.Network
  ```

  Tooyour 계정에 로그인 합니다.

  ```powershell
  Login-AzureRmAccount
  ```

  ExpressRoute 회로 toocreate hello 구독을 선택 합니다.

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Express 경로 회로를 만듭니다.

  Hello 지침 toocreate 따라는 [ExpressRoute 회로](expressroute-howto-circuit-arm.md) hello 연결 공급자가 사용자를 프로 비전 있습니다.

  관리 되는 계층 3 서비스를 제공 하는 연결 공급자, 경우에 연결 공급자 tooenable 있습니다에 대 한 피어 링 개인 Azure를 요청할 수 있습니다. 이 경우 hello 다음 섹션에 나열 된 toofollow 지침 필요 하지는 않습니다. 그러나 연결 공급자 회로 만든 후,에 대 한 라우팅 관리 하지 않는 경우 계속 hello 다음 단계를 사용 하 여 구성 됩니다.
3. Hello ExpressRoute 회로 toomake 프로 비전 되 고도 사용 하도록 설정 되었는지 확인 합니다. 다음 예제는 hello를 사용 합니다.

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  hello 응답은 다음 예제와 비슷한 toohello입니다.

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
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

   다음 예에서는 tooconfigure Microsoft 피어 링 회로 대 한 hello를 사용 합니다.

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a>tooget Microsoft 피어 링 세부 정보

다음 예제는 hello를 사용 하 여 구성 정보를 얻을 수 있습니다.

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft 피어 링 구성

다음 예제는 hello를 사용 하 여 hello 구성의 어떠한 부분을 업데이트할 수 있습니다.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft 피어 링

Hello 다음 cmdlet을 실행 하 여 피어 링 구성을 제거할 수 있습니다.

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a>다음 단계

다음 단계 [연결할 ExpressRoute 회로 VNet tooan](expressroute-howto-linkvnet-arm.md)합니다.

* Express 경로 워크플로에 대한 자세한 내용은 [Express 경로 워크플로](expressroute-workflows.md)를 참조하세요.
* 회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.
* 가상 네트워크 작업에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.
