---
title: "ExpressRoute 회로 만들기 및 수정: PowerShell: Azure 클래식 | Microsoft Docs"
description: "이 문서를 만들고 ExpressRoute 회로 프로 비전에 대 한 hello 단계를 안내 합니다. 또한이 문서를 보면 어떻게 toocheck hello 상태 업데이트 또는 삭제 하 고, 회로가 프로 비전 해제 알 수 있습니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a>PowerShell을 사용하여 ExpressRoute 회로 만들기 및 수정(클래식)
> [!div class="op_single_selector"]
> * [Azure 포털](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [비디오 - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell(클래식)](expressroute-howto-circuit-classic.md)
>

이 문서를 안내해 hello 단계 toocreate Azure ExpressRoute 회로 PowerShell cmdlet 및 hello 클래식 배포 모델을 사용 하 여 합니다. 또한이 문서를 보면 어떻게 toocheck hello 상태 업데이트 또는 삭제 하 고, ExpressRoute 회로 프로 비전 해제 알 수 있습니다.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


**Azure 배포 모델 정보**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>시작하기 전에
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a>1단계. Hello 필수 구성 요소 및 워크플로 기사를 검토 합니다.
Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a>2단계. Hello hello Azure 서비스 관리 (SM) PowerShell 모듈의 최신 버전 설치
Hello 지침에 따라 [Azure PowerShell cmdlet 시작](/powershell/azure/overview) 방법에 대 한 단계별 지침에 대 한 tooconfigure 컴퓨터 toouse hello Azure PowerShell 모듈입니다.

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a>3단계. Tooyour Azure 계정에에서 로그인을 구독 선택
1. 관리자 권한으로 PowerShell 콘솔을 열고 및 tooyour 계정을 연결 합니다. 다음 예제에서는 toohelp 연결한 hello를 사용 합니다.

        Login-AzureRmAccount

2. Hello 계정에 대 한 hello 구독을 확인 합니다.

        Get-AzureRmSubscription

3. 둘 이상의 구독을 보유 하는 경우 toouse hello 구독을 선택 합니다.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. 를 사용 하 여 다음 cmdlet tooadd hello Azure 구독 tooPowerShell hello 클래식 배포 모델에 대 한 합니다.

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a>Express 경로 회로 만들기 및 프로비전
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a>1단계. ExpressRoute에 대 한 hello PowerShell 모듈 가져오기
 이미 수행 hello Azure 및 ExpressRoute 모듈에서 순서 toostart hello ExpressRoute cmdlet을 사용 하 여 hello PowerShell 세션으로 가져와야 합니다. Hello 모듈을 가져올 hello 있었던 위치 설치 tooon 로컬 컴퓨터입니다. Tooinstall hello 모듈을 사용해 hello 방법에 따라, hello 위치 hello 다음 예제와 다를 수 있습니다. 필요한 경우 hello 예제를 수정 합니다.  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2단계. 지원 되는 공급자, 위치 및 대역폭 hello 목록을 가져옵니다.
ExpressRoute 회로 만들기 전에 hello 지원 되는 연결 공급자, 위치 및 대역폭 옵션 목록이 필요 합니다.

PowerShell cmdlet을 hello `Get-AzureDedicatedCircuitServiceProvider` 이후 단계에서 사용 하는이 정보를 반환 합니다.

    Get-AzureDedicatedCircuitServiceProvider

연결 공급자가 여기에 나열 된 경우 toosee를 확인 합니다. Hello 회로 만들 때 나중에 필요 합니다 하기 때문에 다음 정보를 기록해 둡니다.

* 이름
* PeeringLocations
* BandwidthsOffered

이제 준비 toocreate ExpressRoute 회로 것입니다.         

### <a name="step-3-create-an-expressroute-circuit"></a>3단계. Express 경로 회로 만들기
다음 예제는 hello Silicon Valley에 Equinix 통해 toocreate 200 50mbps ExpressRoute 회로 하는 방법을 보여 줍니다. 다른 공급자와 다른 설정을 사용하는 경우, 요청을 수행할 때 해당 정보를 대체합니다.

> [!IMPORTANT]
> ExpressRoute 회로 서비스 키를 발급 하는 hello 순간부터 요금이 청구 됩니다. Hello 연결 공급자가 준비 tooprovision hello 회로이 작업을 수행할 수 있는지 확인 합니다.
> 
> 

hello 다음 새 서비스 키에 대 한 예제 요청은입니다.

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

또는 다음 예제를 사용 하 여 hello toocreate hello premium 추가 기능으로 ExpressRoute 회로 하려는 경우. Toohello 참조 [express 경로 FAQ](expressroute-faqs.md) hello premium 추가 기능에 대 한 자세한 내용은 합니다.

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


hello 응답 hello 서비스 키를 포함 합니다. Hello 다음을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a>4단계. 모든 hello ExpressRoute 회로 나열
Hello를 실행할 수 있습니다 `Get-AzureDedicatedCircuit` tooget 모든 목록이 만든 ExpressRoute 회로 hello 명령:

    Get-AzureDedicatedCircuit

hello 응답에는 다음 예제는 다음과 유사한 toohello 됩니다.

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Hello를 사용 하 여 언제 든 지가이 정보를 검색할 수 `Get-AzureDedicatedCircuit` cmdlet. Hello 매개 변수 없이 호출을 만드는 모든 hello 회로 나열 합니다. 서비스 키 hello에 나열 될 *ServiceKey* 필드입니다.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Hello 다음을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5단계. Hello 서비스 키 tooyour 연결 공급자를 프로 비전에 대 한 보내기
*ServiceProviderProvisioningState* hello hello 서비스 공급자 쪽에 프로 비전의 현재 상태에 대해 설명 합니다. *상태* Microsoft의 hello에 hello 상태를 제공 합니다. 상태를 프로 비전 하는 회로 대 한 자세한 내용은 참조 hello [워크플로](expressroute-workflows.md#expressroute-circuit-provisioning-states) 문서.

새 ExpressRoute 회로 만들 때 다음 상태 hello hello 회로가 됩니다.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


hello 회로 toohello hello 연결 공급자를 사용 하면 hello 진행 중인 경우 상태 뒤에 이동 합니다.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

ExpressRoute 회로에 있어야 하면 toobe 수 toouse에 대 한 상태에 따라 hello 것:

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6단계. Hello 상태 및 hello 회로 키의 hello 상태를 주기적으로 확인
이를 통해 공급자가 회로 활성화를 마치면 알 수 있습니다. Hello 회로 구성한 후 *ServiceProviderProvisioningState* 모양으로 표시 됩니다 *프로 비전 됨* hello 다음 예제와 같이:

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a>7단계. 라우팅 구성 만들기
Toohello 참조 [ExpressRoute 회로 라우팅 구성 (만들고 회로 피어 링 수정)](expressroute-howto-routing-classic.md) 단계별 지침에 대 한 문서입니다.

> [!IMPORTANT]
> 이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다. 관리된 3계층 서비스(일반적으로 MPLS와 같은 IP VPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a>8단계: 가상 네트워크 tooan ExpressRoute 회로 연결
다음으로, 가상 네트워크 tooyour ExpressRoute 회로 연결 합니다. 너무 참조[연결 ExpressRoute 회로 toovirtual 네트워크](expressroute-howto-linkvnet-classic.md) 단계별 지침. ExpressRoute에 대 한 hello 클래식 배포 모델을 사용 하 여 가상 네트워크 toocreate 해야 할 경우 참조 [ExpressRoute에 대 한 가상 네트워크 만들기](expressroute-howto-vnet-portal-classic.md)합니다.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>ExpressRoute 회로의 hello 상태를 가져오기
Hello를 사용 하 여 언제 든 지가이 정보를 검색할 수 `Get-AzureCircuit` cmdlet. Hello 매개 변수 없이 호출을 만드는 모든 hello 회로 나열 합니다.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Hello 서비스 키 매개 변수 toohello 호출으로 전달 하 여 특정 ExpressRoute 회로 대 한 정보를 얻을 수 있습니다.

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


다음 예제는 hello를 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a>Express 경로 회로 수정
연결에 미치는 영향 없이 Express 경로 회로의 특정 속성을 수정할 수 있습니다.

할 수 있는 가동 중지 시간 없이 사용 다음과 같습니다. hello:

* Express 경로 회로에 대해 Express 경로 프리미엄 추가 기능을 사용하거나 사용하지 않을 수 있습니다.
* 증가 hello 대역폭의 ExpressRoute 회로 제공 된 hello 포트에서 용량입니다. 참고는 회로의 대역폭 hello 다운 그레이드는 지원 되지 않습니다. 
* 데이터 요금 tooUnlimited 데이터에서에서 계획을 계량 hello를 변경 합니다. Note 변경 hello 계량 계획에서 무제한 데이터 요금 tooMetered 데이터가 지원 되지 않습니다.
* *Allow Classic Operations*을 활성화하거나 비활성화할 수 있습니다.

Toohello 참조 [express 경로 FAQ](expressroute-faqs.md) 제한 및 제한 사항에 대 한 자세한 내용은 합니다.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute premium 추가 기능
Hello 다음 PowerShell cmdlet을 사용 하 여 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 설정할 수 있습니다.

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

지금 회로 사용 하도록 설정 하는 hello ExpressRoute premium 추가 기능을 갖게 됩니다. Note hello 명령이 성공적으로 실행 되는 즉시 hello premium 추가 기능에 대 한 청구 먼저 됩니다.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute premium 추가 기능
> [!IMPORTANT]
> 이 작업은 hello 표준 회로 대 한 허용 되는 기능 보다 큰 리소스를 사용 하는 경우 실패할 수 있습니다.
> 
> 

#### <a name="considerations"></a>고려 사항

* Toostandard premium에서에서 다운 그레이드 하기 전에 가상 네트워크 연결 된 toohello 회로 hello 수는 10 보다 작은 확인 해야 합니다. 이렇게 하지 않으면 업데이트 요청이 못하며, 프리미엄 요금이 청구 된 hello 수 있습니다.
* 다른 지리적 위치의 모든 가상 네트워크를 연결 해제해야 합니다. 이렇게 하지 않으면 업데이트 요청이 못하며, 프리미엄 요금이 청구 된 hello 수 있습니다.
* 사설 피어링을 위해서는 경로 테이블의 경로가 4000개 미만이어야 합니다. 경로 테이블 크기가 4, 000 경로 보다 큰 경우 hello BGP 세션 삭제 됩니다 하 고 보급된 된 접두사의 hello 수가 4, 000 하위 메뉴를 클릭 될 때까지 했다가 다시 설정할 수 없습니다.

#### <a name="disable-hello-premium-add-on"></a>Hello premium 추가 기능을 사용 하지 않도록 설정
Hello 다음 PowerShell cmdlet을 사용 하 여 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 해제할 수 있습니다.

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>tooupdate hello ExpressRoute 회로 대역폭
Hello 확인 [express 경로 FAQ](expressroute-faqs.md) 지원 공급자에 대 한 대역폭 옵션입니다. 기존 회로 hello 크기 보다 큰는 상태로 유지 됩니다 (회로 생성 되) hello 실제 포트를 사용 하면 모든 크기를 선택할 수 있습니다.

> [!IMPORTANT]
> Hello 기존 포트에서 부적절 한 용량이 있으면 toorecreate hello ExpressRoute 회로 할 수 있습니다. 해당 위치에서 사용할 수 없는 추가 용량 있으면 hello 회로 업그레이드할 수 없습니다.
>
> Hello 중단 없이 ExpressRoute 회로 대역폭을 줄일 수 없습니다. 대역폭을 다운 그레이드 toodeprovision hello ExpressRoute 회로 해야 하 고 새 ExpressRoute 회로 다시 프로 비전 합니다.
> 
> 

#### <a name="resize-a-circuit"></a>회로 크기 조정

필요한 크기를 결정 한 다음 회로 명령 tooresize 다음 hello를 사용할 수 있습니다.

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

회로는 hello Microsoft 쪽 조정 된 됩니다. 이러한 변경의 쪽 toomatch 사용자 연결 공급자 tooupdate 구성을 게 문의 해야 합니다. 이 시점에서 대역폭 옵션에서 업데이트 하는 참고는 먼저 hello에 대 한 청구 있습니다.

Hello hello 회로 대역폭을 늘릴 때 다음 오류가 표시 되 면 것 의미 합니다. 기존 회로 만들 위치 hello 실제 포트에 남아 있는 충분 한 대역폭 없습니다. 이 회로 toodelete 있고 필요한 hello 크기의 새 회로 만들기. 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Express 경로 회로 프로비전 해제 및 삭제

### <a name="considerations"></a>고려 사항

* 이 작업 toosucceed에 대 한 express 경로 회로 hello에서 모든 가상 네트워크 연결을 해제 해야 합니다. 확인 toosee 있는 모든 가상 네트워크가 있는 경우이 작업이 실패 하면 toohello 회로 연결 합니다.
* Hello ExpressRoute 회로 서비스 공급자의 프로비저닝 상태 이면 **프로 비전** 또는 **프로 비전 됨** 편인 서비스 공급자 toodeprovision hello 회로 사용 해야 합니다. Tooreserve 리소스를 계속 하 고 hello 서비스 공급자 프로 비전 해제 hello 회로 완료 하 고 알려주는 될 때까지 사용자를 청구 합니다.
* Hello 서비스 공급자가 회로 hello를 프로 비전 해제 하는 경우 (hello 서비스 공급자 프로 비전 상태가 너무 설정 되어**프로 비전 되지**) hello 회로 삭제할 수 있습니다. Hello 회로 대 한 요금 청구를 중지 합니다.

#### <a name="delete-a-circuit"></a>회로 삭제

Hello 다음 명령을 실행 하 여 ExpressRoute 회로 삭제할 수 있습니다.

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a>다음 단계
회로 만든 후 다음 hello 수행 해야 합니다.

* [Express 경로 회로의 라우팅 만들기 및 수정](expressroute-howto-routing-classic.md)
* [가상 네트워크 tooyour ExpressRoute 회로 연결](expressroute-howto-linkvnet-classic.md)

