---
title: "클래식 tooResource 관리자에서에서 ExpressRoute 회로 이동: PowerShell: Azure | Microsoft Docs"
description: "이 페이지에서는 PowerShell을 사용 하 여 클래식 회로 toohello 리소스 관리자 배포 toomove을 모델링 하는 방법을 설명 합니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a>PowerShell을 사용 하 여 hello 클래식 toohello 리소스 관리자 배포 모델에서 ExpressRoute 회로 이동 합니다.

리소스 관리자 배포 모델 및 클래식 hello에 대 한 ExpressRoute 회로 toouse hello 회로 toohello 리소스 관리자 배포 모델을 이동 해야 합니다. hello 다음 섹션에서는 PowerShell을 사용 하 여 회로 이동 하면 합니다.

## <a name="before-you-begin"></a>시작하기 전에

* Hello Azure PowerShell 모듈의 최신 버전 hello 있는지 확인 하십시오 (이상 버전 1.0). 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
* Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.
* 제공 하는 hello 정보를 검토 [클래식 tooResource 관리자에서에서 ExpressRoute 회로 이동](expressroute-move.md)합니다. 완전히 이해 하는 hello 제한 및 제한 사항이 있는지 확인 합니다.
* Hello 회로 hello 클래식 배포 모델에서 완전 하 게 작동 하는지 확인 합니다.
* Hello 리소스 관리자 배포 모델에서 만든 리소스 그룹 가졌는지 확인 합니다.

## <a name="move-an-expressroute-circuit"></a>ExpressRoute 회로 이동

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a>1 단계: hello 클래식 배포 모델에서 회로 세부 정보를 수집 합니다.

Azure 클래식 환경 toohello에 로그인 하 고 hello 서비스 키를 수집 합니다.

1. Azure 계정 tooyour에 로그인 합니다.

  ```powershell
  Add-AzureAccount
  ```

2. Hello 적절 한 Azure 구독을 선택 합니다.

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. Azure 및 express 경로 대 한 hello PowerShell 모듈을 가져옵니다.

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. 모든 ExpressRoute 회로 대 한 tooget hello 서비스 키 아래의 hello cmdlet을 사용 합니다. Hello 키를 검색 한 후 복사 hello **서비스 키** toomove toohello 리소스 관리자 배포 모델을 사용 하지 않겠다고 hello 회로의 합니다.

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a>2단계: 로그인하여 리소스 그룹 만들기

리소스 관리자 환경을 toohello 하 고 새 리소스 그룹 만들기 합니다.

1. Tooyour Azure Resource Manager 환경에 로그인 합니다.

  ```powershell
  Login-AzureRmAccount
  ```

2. Hello 적절 한 Azure 구독을 선택 합니다.

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. 리소스 그룹을 아직 없는 경우 hello 조각 toocreate 새 리소스 그룹을 수정 합니다.

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a>3 단계: hello ExpressRoute 회로 toohello 리소스 관리자 배포 모델을 이동

사용자는 이제 준비 toomove hello 클래식 배포 모델 toohello 리소스 관리자 배포 모델에서 express 경로 회로입니다. 계속 하기 전에 제공 하는 hello 정보를 검토 [hello 클래식 toohello 리소스 관리자 배포 모델에서 ExpressRoute 회로 이동](expressroute-move.md)합니다.

toomove 회로 수정 하 고 다음 코드 조각 hello 실행:

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> Hello 이동 완료 되 면 hello 이전 cmdlet에 나열 된 hello 새 이름을 사용 하는 tooaddress hello 리소스 됩니다. hello 회로 기본적으로 바뀝니다.
> 

## <a name="modify-circuit-access"></a>회로 액세스 수정

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a>두 가지 경우 모두에 대 한 express 경로 회로 액세스 tooenable

클래식 express 경로 회로 toohello 리소스 관리자 배포 모델을 이동한 후 액세스 tooboth 배포 모델을 사용할 수 있습니다. Hello cmdlet tooenable 액세스 tooboth 배포 모델을 따라를 실행 합니다.

1. Hello 회로 세부 정보를 가져옵니다.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. "클래식 작업 허용" tooTRUE를 설정 합니다.

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. Hello 회로 업데이트 합니다. 이 작업을 성공적으로 완료 되 면 hello 클래식 배포 모델에서 수 tooview hello 회로 됩니다.

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. 다음 cmdlet tooget hello ExpressRoute 회로의 세부 정보 hello hello를 실행 합니다. 나열 된 수 toosee hello 서비스 키 여야 합니다.

  ```powershell
  get-azurededicatedcircuit
  ```

5. 이제 클래식 Vnet 및 hello 리소스 관리자 명령에 대 한 hello 클래식 배포 모델 명령을 사용 하 여 리소스 관리자 Vnet에 대 한 링크 toohello ExpressRoute 회로 관리할 수 있습니다. hello 다음 문서는 데 도움이 링크 toohello ExpressRoute 회로 관리 합니다.

    * [가상 네트워크 tooyour hello 리소스 관리자 배포 모델에서 ExpressRoute 회로 연결](expressroute-howto-linkvnet-arm.md)
    * [가상 네트워크 tooyour hello 클래식 배포 모델의 ExpressRoute 회로 연결](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a>toodisable ExpressRoute 회로 액세스 toohello 클래식 배포 모델

Hello cmdlet toodisable 액세스 toohello 클래식 배포 모델을 실행 합니다.

1. Hello ExpressRoute 회로의 세부 정보를 가져옵니다.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. "클래식 작업 허용" tooFALSE를 설정 합니다.

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. Hello 회로 업데이트 합니다. 이 작업을 성공적으로 완료 되 면 hello 클래식 배포 모델에서 수 tooview hello 회로 되지 않습니다.

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a>다음 단계

* [Express 경로 회로의 라우팅 만들기 및 수정](expressroute-howto-routing-arm.md)
* [가상 네트워크 tooyour ExpressRoute 회로 연결](expressroute-howto-linkvnet-arm.md)
