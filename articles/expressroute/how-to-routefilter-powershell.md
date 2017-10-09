---
title: "Azure ExpressRoute Microsoft 피어링에 대한 경로 필터 구성: PowerShell | Microsoft Docs"
description: "이 문서에서는 PowerShell을 사용 하 여 Microsoft 피어 링에 대 한 tooconfigure 경로 필터 하는 방법을 설명합니다"
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Microsoft 피어링에 대한 경로 필터 구성

경로 필터는 방식으로 tooconsume Microsoft 피어 링을 통해 지원 되는 서비스의 하위 집합입니다. 이 문서 도움말 구성 하 고 ExpressRoute 회로 대 한 경로 필터 관리에 hello 안내 합니다.

Dynamics 365 서비스 및 비즈니스에 대 한 Exchange Online, SharePoint Online 및 Skype와 같은 Office 365 서비스는 hello Microsoft 피어 링을 통해 액세스할 수 있습니다. Microsoft 피어 링 express 경로 회로에 구성 되 면 모든 접두사 관련된 toothese 서비스는 설정 된 hello BGP 세션을 통해 보급 합니다. BGP 커뮤니티 값은 연결 된 tooevery 접두사 tooidentify hello 서비스 hello 접두사를 통해 제공 된입니다. Hello BGP 커뮤니티 값과 매핑되는 hello 서비스의 목록에 대 한 참조 [BGP 커뮤니티](expressroute-routing.md#bgp)합니다.

연결 tooall 서비스를 필요로 하는 경우 많은 수의 접두사는 BGP를 통해 보급 합니다. 이 네트워크 라우터에서 관리 hello 경로 테이블의 hello 크기 크게 증가 합니다. Microsoft 피어 링을 통해 제공 되는 서비스의 하위 집합만 tooconsume 하려는 경우 두 가지 방법으로 경로 테이블의 hello 크기를 줄일 수 있습니다. 다음을 수행할 수 있습니다.

- BGP 커뮤니티에 라우팅 필터를 적용하여 필요 없는 접두사를 필터링합니다. 표준 네트워킹 방법은 많은 네트워크 내에서 일반적으로 사용됩니다.

- 경로 필터를 정의 하 고 tooyour ExpressRoute 회로 적용 합니다. 경로 필터는 새 리소스의 hello 목록을 선택할 수 있습니다 서비스를 Microsoft 피어 링을 통해 tooconsume 계획입니다. ExpressRoute 라우터는만 hello hello 경로 필터에서 식별 된 toohello 서비스에 속하는 접두사 목록을 보냅니다.

### <a name="about"></a>경로 필터 정보

Microsoft 피어 링 express 경로 회로에 구성 되 면 hello Microsoft에 지 라우터는 한 쌍의 BGP 세션을 원하는 대로 이동해 왔거나 연결 공급자의에 지 라우터를 hello 설정 합니다. 경로가 보급된 tooyour 네트워크입니다. tooenable 경로 광고 tooyour 네트워크 경로 필터를 연결 해야 합니다.

경로 필터를 사용 하면 ExpressRoute 회로 Microsoft 피어 링을 통해 tooconsume 서비스를 식별할 수 있습니다. 모든 hello BGP 커뮤니티 값의 허용 목록을 경우합니다 경로 필터 리소스 정의 tooan ExpressRoute 회로 연결 되 면 toohello BGP 커뮤니티 값에 매핑되는 모든 접두사는 보급된 tooyour 네트워크입니다.

Office 365 서비스에 toobe 수 tooattach 경로 필터, ExpressRoute 통해 권한 부여 tooconsume Office 365 서비스 있어야 합니다. ExpressRoute 통해 권한 있는 tooconsume Office 365 서비스에 없으면 hello 작업 tooattach 경로 필터 실패 합니다. Hello 권한 부여 프로세스에 대 한 자세한 내용은 참조 [Office 365에 대 한 Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)합니다. 연결 tooDynamics 365 서비스에 모든 권한을 가지 지 필요 하지 않습니다.

> [!IMPORTANT]
> 이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다. Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다.
> 
> 

### <a name="workflow"></a>워크플로

toobe 수 toosuccessfully Microsoft 피어 링을 통해 tooservices 연결, hello 다음 구성 단계를 완료 해야 합니다.

- Microsoft 피어링을 프로비전하는 활성 ExpressRoute 회로가 있어야 합니다. 이러한 작업 지침 tooaccomplish 다음 hello를 사용할 수 있습니다.
  - [ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다. ExpressRoute 회로 hello 가능 하 고 프로 비전 된 상태에 있어야 합니다.
  - [Microsoft 피어 링 만들기](expressroute-circuit-peerings.md) 직접 hello BGP 세션을 관리 하는 경우. 또는 연결 공급자가 회로에 Microsoft 피어링을 프로비전하도록 합니다.

-  경로 필터를 만들고 구성해야 합니다.
    - 식별 hello tooconsume Microsoft 피어 링을 통해 서비스
    - Hello 서비스와 관련 된 BGP 커뮤니티 값의 hello 목록 확인
    - 한 규칙 tooallow hello 접두사 목록 일치 하는 hello BGP 커뮤니티 값을 만듭니다.

-  Hello 경로 필터 toohello ExpressRoute 회로 연결 해야 합니다.

## <a name="before-you-begin"></a>시작하기 전에

구성을 시작 하기 전에 hello 다음 조건을 충족 하는지 확인 합니다.

 - Hello hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전을 설치 합니다. 자세한 내용은 [Azure PowerShell 설치 및 구성](/powershell/azure/install-azurerm-ps)을 참조하세요.

  > [!NOTE]
  > Hello 설치 관리자를 사용 하 여 보다는 hello PowerShell 갤러리에서 hello 최신 버전을 다운로드 합니다. 현재 설치 관리자 hello hello 필요한 cmdlet을 지원 하지 않습니다.
  > 

 - 검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.

 - 활성화된 Express 경로 회로가 있어야 합니다. 너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다. ExpressRoute 회로 hello 가능 하 고 프로 비전 된 상태에 있어야 합니다.

 - 활성 Microsoft 피어링이 있어야 합니다. [피어링 구성 수정 및 만들기](expressroute-circuit-peerings.md)의 지침에 따릅니다.

### <a name="log-in-tooyour-azure-account"></a>Azure 계정 tooyour에 로그인

이 구성을 시작 하기 전에 tooyour Azure 계정에에서 로그인 해야 합니다. hello cmdlet Azure 계정에 대 한 hello 로그인 자격 증명을 묻습니다. 로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정을 다운로드 합니다.

상승 된 권한으로 PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다. 다음 예제에서는 toohelp 연결한 hello를 사용 합니다.

```powershell
Login-AzureRmAccount
```

여러 Azure 구독이 있는 경우 hello 계정에 대 한 hello 구독을 확인 합니다.

```powershell
Get-AzureRmSubscription
```

Toouse hello 구독을 지정 합니다.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="prefixes"></a>1단계. 접두사 및 BGP 커뮤니티 값의 목록 가져오기

### <a name="1-get-a-list-of-bgp-community-values"></a>1. BGP 커뮤니티 값의 목록 가져오기

관련 된 접두사 목록을 hello 및 hello Microsoft 피어 링을 통해 액세스할 수 있는 서비스와 관련 된 BGP 커뮤니티 값 목록이 tooget hello cmdlet을 다음 사용:

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. 원하는 toouse hello 값 목록을 확인합니다

Hello 경로 필터에 원하는 BGP 커뮤니티 값 목록이 toouse을 만듭니다. 예를 들어 hello Dynamics 365 서비스에 대 한 BGP 커뮤니티 값 12076:5040 됩니다.

## <a name="filter"></a>2단계. 경로 필터 및 필터 규칙 만들기

경로 필터 규칙을 하나만 가질 수 있습니다 및 hello 규칙 '허용' 형식 이어야 합니다. 이 규칙에는 관련된 BGP 커뮤니티 값의 목록이 있을 수 있습니다

### <a name="1-create-a-route-filter"></a>1. 경로 필터 만들기

먼저 hello 경로 필터를 만듭니다. hello 명령 ' 새로 만들기-AzureRmRouteFilter'만 경로 필터 리소스를 만듭니다. Hello 리소스를 만든 후 다음 규칙을 만들고 해야 toohello 경로 필터 개체를 연결 합니다. 경로 필터 리소스 hello 명령 toocreate 다음을 실행 합니다.

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a>2. 필터 규칙 만들기

Hello 예제와 같이 쉼표로 구분 된 목록으로 BGP 커뮤니티의 집합을 지정할 수 있습니다. 다음 명령은 toocreate hello 새 규칙을 실행 합니다.
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a>3. Hello 규칙 toohello 경로 필터를 추가 합니다.

다음 명령 tooadd hello 필터 규칙 toohello 경로 필터 hello를 실행 합니다.
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="attach"></a>3단계. Hello 경로 필터 tooan ExpressRoute 회로 연결

Hello 명령 tooattach hello 경로 필터 toohello ExpressRoute 회로 유일한 Microsoft 피어 링 했 고 다음을 실행 합니다.

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="getproperties"></a>경로 필터의 tooget hello 속성

경로 필터의 tooget hello 속성 단계를 수행 하는 hello를 사용 합니다.

1. 다음 명령은 tooget hello 경로 필터 리소스 hello를 실행 합니다.

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. Hello 다음 명령을 실행 하 여 hello 경로 필터 리소스에 대 한 hello 경로 필터 규칙을 가져옵니다.

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <a name="updateproperties"></a>경로 필터의 tooupdate hello 속성

Hello 경로 필터는 이미 연결 되어 있는 경우 회로 tooa 업데이트 toohello BGP 커뮤니티 목록을 자동으로 설정 하는 hello BGP 세션을 통해 적절 한 접두사 광고 변경 내용을 전파 합니다. 다음 명령을 hello를 사용 하 여 경로 필터 목록이 BGP 커뮤니티 hello를 업데이트할 수 있습니다.

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="detach"></a>ExpressRoute 회로에서 경로 필터 toodetach

경로 필터 hello ExpressRoute 회로에서 분리 되 면 접두사가 hello BGP 세션을 통해 보급 합니다. 필터에서 다음 명령을 hello를 사용 하 여 ExpressRoute 회로 분리할 수 있습니다.
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="delete"></a>경로 필터 toodelete

삭제 되지 않았으면 경로 필터 tooany 회로 연결에 할 수 있습니다. 해당 hello 경로 필터 되지 않도록 tooany 회로 toodelete 시도 하기 전에 연결 된 것입니다. 다음 명령을 hello를 사용 하 여 필터를 삭제할 수 있습니다.

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a>다음 단계

ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.
