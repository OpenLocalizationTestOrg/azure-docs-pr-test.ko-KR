---
title: "ExpressRoute 회로 만들기 및 수정: PowerShell: Azure Resource Manager | Microsoft Docs"
description: "이 문서에서는 어떻게 toocreate, 프로 비전, 확인, 업데이트, 삭제 및 ExpressRoute 회로 프로 비전 해제를 설명 합니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>PowerShell을 사용하여 Express 경로 회로 만들기 및 수정
> [!div class="op_single_selector"]
> * [Azure 포털](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [비디오 - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell(클래식)](expressroute-howto-circuit-classic.md)
>

이 문서에서는 PowerShell cmdlet 및 hello Azure 리소스 관리자 배포 모델을 사용 하 여 toocreate Azure ExpressRoute 회로 하는 방법을 설명 합니다. 또한이 문서를 보면 hello 회로의 toocheck hello 상태를 업데이트 또는 삭제 및 프로 비전 해제 방법을 알 수 있습니다.

## <a name="before-you-begin"></a>시작하기 전에
* Hello hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전을 설치 합니다. 자세한 내용은 [Azure PowerShell 개요](/powershell/azure/overview)를 참조하세요.
* 검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.


## <a name="create-and-provision-an-expressroute-circuit"></a>Express 경로 회로 만들기 및 프로비전
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Tooyour Azure 계정에에서 로그인 하 고 구독을 선택 합니다.
toobegin 구성, tooyour Azure 계정에에서 로그인 합니다. 예제 toohelp 연결한 다음 hello를 사용 합니다.

```powershell
Login-AzureRmAccount
```

Hello 계정에 대 한 hello 구독을 확인 합니다.

```powershell
Get-AzureRmSubscription
```

Hello 피드에 toocreate에 대 한 express 경로 회로 선택 합니다.

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. 지원 되는 공급자, 위치 및 대역폭 hello 목록을 가져옵니다.
ExpressRoute 회로 만들기 전에 hello 지원 되는 연결 공급자, 위치 및 대역폭 옵션 목록이 필요 합니다.

PowerShell cmdlet을 hello **Get AzureRmExpressRouteServiceProvider** 이후 단계에서 사용 하는이 정보를 반환 합니다.

```powershell
Get-AzureRmExpressRouteServiceProvider
```

연결 공급자가 여기에 나열 된 경우 toosee를 확인 합니다. Hello 다음 정보를 기록해 둡니다. 나중에 회로를 만들 때 필요합니다.

* 이름
* PeeringLocations
* BandwidthsOffered

이제 준비 toocreate ExpressRoute 회로 것입니다.   

### <a name="3-create-an-expressroute-circuit"></a>3. Express 경로 회로 만들기
아직 리소스 그룹이 없는 경우 Express 경로 회로를 만들기 전에 먼저 리소스 그룹을 만들어야 합니다. 따라서 hello 다음 명령을 실행 하 여 수행할 수 있습니다.

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


다음 예제는 hello Silicon Valley에 Equinix 통해 toocreate 200 50mbps ExpressRoute 회로 하는 방법을 보여 줍니다. 다른 공급자와 다른 설정을 사용하는 경우, 요청을 수행할 때 해당 정보를 대체합니다. hello 다음 새 서비스 키에 대 한 예제 요청은입니다.

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

Hello 올바른 SKU 계층과 SKU 제품군을 지정 하 고 있는지 확인 합니다.

* SKU 계층은 Express 경로 표준 또는 Express 경로 Premium 추가 기능이 사용되는지 여부를 결정합니다. 지정할 수 있습니다 *표준* tooget hello 표준 SKU 또는 *프리미엄* hello premium 추가 기능에 대 한 합니다.
* SKU 제품군 hello 청구 유형을 결정합니다. 데이터 요금제의 경우 *Metereddata*를 선택하고 무제한 데이터 요금제의 경우 *Unlimiteddata*를 선택할 수 있습니다. hello 청구 유형을 변경할 수 있습니다 *Metereddata* 너무*Unlimiteddata*에서 hello 형식은 변경할 수 있지만 *Unlimiteddata* 너무*Metereddata* .

> [!IMPORTANT]
> ExpressRoute 회로 서비스 키를 발급 하는 hello 순간부터 요금이 청구 됩니다. Hello 연결 공급자가 준비 tooprovision hello 회로이 작업을 수행할 수 있는지 확인 합니다.
> 
> 

hello 응답 hello 서비스 키를 포함합니다. Hello 다음 명령을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4. 모든 Express 경로 회로 나열
모든 목록이 hello ExpressRoute 회로 사용자가 만든 tooget 실행 hello **Get AzureRmExpressRouteCircuit** 명령:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

hello 응답 다음 예제와 비슷한 toohello 볼 수 있습니다.

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

Hello를 사용 하 여 언제 든 지가이 정보를 검색할 수 `Get-AzureRmExpressRouteCircuit` cmdlet. Hello 매개 변수 없이 호출을 만드는 모든 hello 회로 나열 합니다. 서비스 키 hello에 나열 될 *ServiceKey* 필드:

```powershell
Get-AzureRmExpressRouteCircuit
```


hello 응답 다음 예제와 비슷한 toohello 볼 수 있습니다.

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Hello 다음 명령을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Hello 서비스 키 tooyour 연결 공급자를 프로 비전에 대 한 보내기
*ServiceProviderProvisioningState* hello hello 서비스 공급자 쪽에 프로 비전의 현재 상태에 대 한 정보를 제공 합니다. 상태는 Microsoft의 hello에 hello 상태를 제공합니다. 상태를 프로 비전 하는 회로 대 한 자세한 내용은 참조 hello [워크플로](expressroute-workflows.md#expressroute-circuit-provisioning-states) 문서.

새 ExpressRoute 회로 만들 때 다음 상태 hello hello 회로가 됩니다.

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



hello 회로 toohello hello 연결 공급자를 사용 하면 hello 진행 중인 경우 뒤에 상태를 변경 합니다.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

하면 toobe 수 toouse ExpressRoute 회로 hello 상태 뒤에 있어야 합니다.

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Hello 상태 및 hello 회로 키의 hello 상태를 주기적으로 확인
Hello 상태 및 hello 회로 키의 hello 상태를 확인 하면 공급자가 회로 설정 하는 때를 알 수 있습니다. Hello 회로 구성한 후 *ServiceProviderProvisioningState* 로 표시 *프로 비전 됨*hello 다음 예제에에서 나온 것 처럼:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


hello 응답 다음 예제와 비슷한 toohello 볼 수 있습니다.

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

### <a name="7-create-your-routing-configuration"></a>7. 라우팅 구성 만들기
단계별 지침은 hello [ExpressRoute 회로 라우팅 구성을](expressroute-howto-routing-arm.md) toocreate 문서 및 회로 피어 링을 수정 합니다.

> [!IMPORTANT]
> 이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다. 관리된 3계층 서비스(일반적으로 MPLS와 같은 IP VPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. 가상 네트워크 tooan ExpressRoute 회로 연결
다음으로, 가상 네트워크 tooyour ExpressRoute 회로 연결 합니다. 사용 하 여 hello [tooExpressRoute 회로 네트워크 연결 가상](expressroute-howto-linkvnet-arm.md) hello 리소스 관리자 배포 모델을 사용 하 여 작업할 때 문서입니다.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>ExpressRoute 회로의 hello 상태를 가져오기
Hello를 사용 하 여 언제 든 지가이 정보를 검색할 수 **Get AzureRmExpressRouteCircuit** cmdlet. Hello 매개 변수 없이 호출을 만드는 모든 hello 회로 나열 합니다.

```powershell
Get-AzureRmExpressRouteCircuit
```


hello 응답에는 다음 예제와 비슷한 toohello 됩니다.

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


Hello 리소스 그룹 이름 및 회로 이름 매개 변수 toohello 호출으로 전달 하 여 특정 ExpressRoute 회로 대 한 정보를 얻을 수 있습니다.

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


hello 응답 다음 예제와 비슷한 toohello 볼 수 있습니다.

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


Hello 다음 명령을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a>Express 경로 회로 수정
연결에 미치는 영향 없이 Express 경로 회로의 특정 속성을 수정할 수 있습니다.

할 수 있는 가동 중지 시간 없이 사용 다음과 같습니다. hello:

* Express 경로 회로에 대해 Express 경로 프리미엄 추가 기능을 사용하거나 사용하지 않을 수 있습니다.
* 증가 hello 대역폭의 ExpressRoute 회로 제공 된 hello 포트에서 용량입니다. 회로의 대역폭 hello를 다운 그레이드는 지원 되지 않습니다. 
* 데이터 요금 tooUnlimited 데이터에서에서 계획을 계량 hello를 변경 합니다. 무제한 데이터 요금 tooMetered 데이터가 지원 되지 않습니다에서 계획을 계량 hello를 변경 합니다.
* *Allow Classic Operations*을 활성화하거나 비활성화할 수 있습니다.

제한 및 제한 사항에 대 한 자세한 내용은 참조 toohello [express 경로 FAQ](expressroute-faqs.md)합니다.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute premium 추가 기능
다음 PowerShell 코드 조각을 hello를 사용 하 여 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 설정할 수 있습니다.

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

지금 hello 회로 사용 하도록 설정 하는 hello ExpressRoute premium 추가 기능을 갖게 됩니다. Hello 명령이 성공적으로 실행 되는 즉시 hello premium 추가 기능에 대 한 청구 하기 시작할 예정입니다.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute premium 추가 기능
> [!IMPORTANT]
> 이 작업은 hello 표준 회로 대 한 허용 되는 기능 보다 큰 리소스를 사용 하는 경우 실패할 수 있습니다.
> 
> 

참고 hello 다음.

* 연결 된 가상 네트워크의 해당 hello 수를 확인 해야 toostandard premium에서에서 다운 그레이드 먼저 toohello 회로 10 보다 작은 합니다. 그렇게 하지 않으면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.
* 다른 지리적 위치의 모든 가상 네트워크를 연결 해제해야 합니다. 그렇게 하지 않으면 업데이트 요청이 실패하고, 프리미엄 요금이 청구됩니다.
* 사설 피어링을 위해서는 경로 테이블의 경로가 4000개 미만이어야 합니다. 경로 테이블 크기가 4, 000 경로 보다 큰 경우 hello BGP 세션 삭제 하 고 보급된 된 접두사의 hello 수가 4, 000 하위 메뉴를 클릭 될 때까지 했다가 다시 설정할 수 없습니다.

Hello 다음 PowerShell cmdlet을 사용 하 여 hello 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 해제할 수 있습니다.

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>tooupdate hello ExpressRoute 회로 대역폭
공급자에서 지원 되는 대역폭 옵션에 대 한 확인 hello [express 경로 FAQ](expressroute-faqs.md)합니다. 기존 회로 hello 크기 보다 큰 모든 크기를 선택할 수 있습니다.

> [!IMPORTANT]
> Hello 기존 포트에서 부적절 한 용량이 있으면 toorecreate hello ExpressRoute 회로 할 수 있습니다. 해당 위치에서 사용할 수 없는 추가 용량 있으면 hello 회로 업그레이드할 수 없습니다.
>
> Hello 중단 없이 ExpressRoute 회로 대역폭을 줄일 수 없습니다. 대역폭을 다운 그레이드 toodeprovision hello ExpressRoute 회로 해야 하 고 새 ExpressRoute 회로 다시 프로 비전 합니다.
> 

필요한 크기를 결정 한 후 다음 명령 tooresize hello 회로 사용 합니다.

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


회로 hello Microsoft 쪽에 조정 됩니다. 다음 문의 해야 해당 측 toomatch 사용자 연결 공급자 tooupdate 구성을이 변경 합니다. 이 알림은 변경한 후 업데이트 하는 hello 대역폭 옵션에 대 한 청구 있습니다 하기 시작할 예정입니다.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>요금제 toounlimited에서 toomove hello SKU
다음 PowerShell 코드 조각을 hello를 사용 하 여 hello ExpressRoute 회로의 SKU를 변경할 수 있습니다.

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>toocontrol 액세스 toohello 클래식 및 리소스 관리자 환경
지침에 hello 검토 [hello 클래식 toohello 리소스 관리자 배포 모델의 이동 ExpressRoute 회로](expressroute-howto-move-arm.md)합니다.  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Express 경로 회로 프로비전 해제 및 삭제
참고 hello 다음.

* ExpressRoute 회로 hello에서 모든 가상 네트워크 연결을 해제 해야 합니다. 이 작업이 실패 하면 가상 네트워크가 있는 경우 toosee toohello 회로 연결을 확인 합니다.
* Hello ExpressRoute 회로 서비스 공급자의 프로비저닝 상태 이면 **프로 비전** 또는 **프로 비전 됨** 편인 서비스 공급자 toodeprovision hello 회로 사용 해야 합니다. Tooreserve 리소스를 계속 하 고 hello 서비스 공급자 프로 비전 해제 hello 회로 완료 하 고 알려주는 될 때까지 사용자를 청구 합니다.
* Hello 서비스 공급자가 회로 hello를 프로 비전 해제 하는 경우 (hello 서비스 공급자 프로 비전 상태가 너무 설정 되어**프로 비전 되지**) hello 회로 삭제할 수 있습니다. 이렇게 되 면 hello 회로 대 한 청구

Hello 다음 명령을 실행 하 여 ExpressRoute 회로 삭제할 수 있습니다.

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>다음 단계

회로 만든 후 다음 hello 수행 해야 합니다.

* [Express 경로 회로의 라우팅 만들기 및 수정](expressroute-howto-routing-arm.md)
* [가상 네트워크 tooyour ExpressRoute 회로 연결](expressroute-howto-linkvnet-arm.md)
