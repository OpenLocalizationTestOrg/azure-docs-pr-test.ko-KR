---
title: "aaaUsing PowerShell toomanage azure에서 트래픽 관리자 | Microsoft Docs"
description: "Azure Resource Manager과 함께 Traffic Manager용 powershell 사용"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>PowerShell toomanage 트래픽 관리자를 사용 하 여

Azure 리소스 관리자는 Azure에서 서비스에 대 한 hello 기본 설정된 관리 인터페이스입니다. Azure Resource Manager 기반 API 및 도구를 사용하여 Azure Traffic Manager 프로파일을 관리할 수 있습니다.

## <a name="resource-model"></a>리소스 모델

Azure Traffic Manager는 Traffic Manager 프로필을 호출하는 설정 모음을 사용하여 구성됩니다. 이 프로필에 DNS 설정, 트래픽 라우팅 설정, 끝점 모니터링 설정을 포함 하 고 서비스 끝점 toowhich 트래픽 목록은 라우팅됩니다.

각 Traffic Manager 프로필은 'TrafficManagerProfiles' 유형의 리소스로 표시됩니다. Hello REST API 수준에서 각 프로필에 대 한 hello URI는 다음과 같습니다.

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Azure PowerShell 설정

이러한 지침은 Microsoft Azure PowerShell을 사용합니다. hello 다음 문서에서는 설명 어떻게 tooinstall 및 Azure PowerShell을 구성 합니다.

* [어떻게 tooinstall Azure PowerShell 및 구성](/powershell/azure/overview)

이 문서의 hello 예제에서는 기존 리소스 그룹 있다고 가정 합니다. 다음 명령을 hello를 사용 하 여 리소스 그룹을 만들 수 있습니다.

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> Azure Resource Manager를 사용하려면 모든 리소스 그룹에 위치가 있어야 합니다. 이 위치는 해당 리소스 그룹에 생성 된 리소스에 대 한 hello 기본으로 사용 됩니다. 그러나 트래픽 관리자 프로필 리소스, 글로벌 국가별 하지 않으므로 hello 다양 한 리소스 그룹 위치에 아무런 영향을 주지 Azure 트래픽 관리자.

## <a name="create-a-traffic-manager-profile"></a>Traffic Manager 프로필 만들기

toocreate 트래픽 관리자 프로필을 사용 하 여 hello `New-AzureRmTrafficManagerProfile` cmdlet:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

다음 표에서 hello hello 매개 변수를 설명 합니다.

| 매개 변수 | 설명 |
| --- | --- |
| 이름 |트래픽 관리자 프로필 리소스 hello에 대 한 hello 리소스 이름입니다. 프로필에 hello 동일한 리소스 그룹 이름은 고유 해야 합니다. 이 이름은 hello DNS 이름 DNS 쿼리에 사용 되는 별개입니다. |
| ResourceGroupName |hello 리소스 그룹 포함 hello 프로필 리소스의 hello 이름입니다. |
| TrafficRoutingMethod |Hello 트래픽 라우팅을 사용 하는 방법 toodetermine 끝점 DNS 쿼리 응답에서 반환 되를 지정 합니다. 가능한 값은 '성능', '가중' 또는 '우선 순위'입니다. |
| RelativeDnsName |이 트래픽 관리자 프로필에서 제공 하는 hello DNS 이름의 hello 호스트 이름 부분을 지정 합니다. 이 값은 hello 프로필의 Azure 트래픽 관리자 tooform hello 정규화 된 도메인 이름 (FQDN)에서 사용 하는 hello DNS 도메인 이름으로 결합 됩니다. 예를 들어 'contoso.trafficmanager.net입니다.'은 'contoso' hello 값 설정 |
| TTL |DNS 시간 to Live (TTL) hello 초 단위로 지정 합니다. 이 ttl hello 로컬 DNS 확인자 및 DNS 클라이언트가 트래픽 관리자 프로필에 대 한 시간 toocache DNS 응답 합니다. |
| MonitorProtocol |Hello 프로토콜 toouse toomonitor 끝점 상태를 지정합니다. 가능한 값은 ‘HTTP’ 및 ‘HTTPS’입니다. |
| MonitorPort |Toomonitor 끝점 상태를 사용 하는 hello TCP 포트를 지정 합니다. |
| MonitorPath |끝점 상태에 대 한 tooprobe를 사용 하는 hello 경로 상대 toohello 끝점 도메인 이름을 지정 합니다. |

hello cmdlet azure에서 트래픽 관리자 프로필을 만들고 해당 프로필 개체 tooPowerShell를 반환 합니다. 이 시점에서 hello 프로필에는 끝점이 없습니다. Tooa 트래픽 관리자 프로필 끝점을 추가 하는 방법에 대 한 자세한 내용은 참조 [트래픽 관리자 끝점 추가](#adding-traffic-manager-endpoints)합니다.

## <a name="get-a-traffic-manager-profile"></a>Traffic Manager 프로필 가져오기

tooretrieve 기존 트래픽 관리자 프로필 개체를 사용 하 여 hello `Get-AzureRmTrafficManagerProfle` cmdlet:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

이 cmdlet은 Traffic Manager 프로필 개체를 반환합니다.

## <a name="update-a-traffic-manager-profile"></a>Traffic Manager 프로필 업데이트

Traffic Manager 프로필을 수정하려면 3 단계 프로세스를 따릅니다.

1. 사용 하 여 검색 hello 프로필 `Get-AzureRmTrafficManagerProfile` 반환한 hello 프로필을 사용 하거나 `New-AzureRmTrafficManagerProfile`합니다.
2. Hello 프로필을 수정 합니다. 끝점을 추가 및 제거하거나 끝점 또는 프로필 매개 변수를 변경할 수 있습니다. 이러한 변경은 오프라인 작업입니다. Hello 로컬 개체 hello 프로필을 나타내는 메모리에만 변경 됩니다.
3. Hello를 사용 하 여 변경 내용을 커밋하여 `Set-AzureRmTrafficManagerProfile` cmdlet.

Hello 프로필의 RelativeDnsName 제외 하 고 모든 프로필 속성을 변경할 수 있습니다. toochange RelativeDnsName hello, 프로필 및 새 이름으로 새 프로필을 삭제 해야 합니다.

다음 예제는 hello toochange 프로필의 TTL hello 하는 방법을 보여 줍니다.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Traffic Manager 끝점에는 세 가지 종류가 있습니다.

1. **Azure 끝점** 은 Azure에서 호스팅되는 서비스입니다.
2. **외부 끝점**은 Azure 외부에서 호스트되는 서비스입니다.
3. **끝점에 중첩 된** 은 트래픽 관리자 프로필의 사용 되는 tooconstruct 중첩 된 계층입니다. 중첩 끝점은 복잡한 응용 프로그램에 대한 고급 트래픽 라우팅 구성을 사용하도록 설정합니다.

세 가지 경우 모두, 끝점은 두 가지 방법으로 추가될 수 있습니다.

1. 앞에서 설명한 3 단계 프로세스를 사용합니다. 이 방법의 장점은 hello는 단일 업데이트에서 여러 끝점 변경을 지정할 수 있습니다.
2. Hello 새로 AzureRmTrafficManagerEndpoint cmdlet을 사용 합니다. 이 cmdlet은 단일 작업으로 끝점 tooan 기존 트래픽 관리자 프로필을 추가합니다.

## <a name="adding-azure-endpoints"></a>Azure 끝점 추가

Azure 끝점는 Azure에서 호스팅되는 서비스를 나타냅니다. 두 가지 유형의 Azure 끝점이 지원됩니다.

1. Azure 웹앱
2. Azure PublicIpAddress 리소스 (연결 된 tooa 부하 분산 장치 또는 가상 컴퓨터 NIC 일 수 있음). hello PublicIpAddress toobe 트래픽 관리자에서 사용 되는 할당 된 DNS 이름이 있어야 합니다.

각 경우에 다음이 해당됩니다.

* hello 서비스의 hello 'targetResourceId' 매개 변수를 사용 하 여 지정 `Add-AzureRmTrafficManagerEndpointConfig` 또는 `New-AzureRmTrafficManagerEndpoint`합니다.
* hello 'Target' 및 'EndpointLocation'에서 암시 된 hello TargetResourceId 합니다.
* '가중치' hello 지정 선택 사항입니다. 가중치는 hello 프로필은 구성 된 toouse hello '가 중' 트래픽 라우팅 방법을 하는 경우에 사용 됩니다. 그렇지 않으면 무시됩니다. 를 지정 하는 경우 hello 값 1에서 1000 사이의 숫자 여야 합니다. hello 기본값은 '1'입니다.
* 지정 하 여 hello 'Priority' 선택 사항입니다. 우선 순위는 hello 프로필은 구성 된 toouse hello 'Priority' 트래픽 라우팅 방법을 하는 경우에 사용 됩니다. 그렇지 않으면 무시됩니다. 유효한 값은 상위 우선 순위를 나타내는 값이 낮은 1 too1000에서은 합니다. 한 끝점에 대해 지정한 경우 모든 끝점에 대해 지정되어야 합니다. 생략 하면 기본값은 '1'에서 시작 하는 hello 끝점이 표시 되지 hello 순서로 적용 됩니다.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>예시 1: `Add-AzureRmTrafficManagerEndpointConfig`을 사용하여 웹앱 끝점 추가

이 예제에서는에서는 트래픽 관리자 프로필을 만들고 추가 hello를 사용 하 여 두 개의 웹 응용 프로그램 끝점 `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>예시 2: `New-AzureRmTrafficManagerEndpoint`을 사용하여 publicIpAddress 끝점 추가

이 예제에서는 공용 IP 주소 리소스 toohello 트래픽 관리자 프로필을 추가 됩니다. hello 공용 IP 주소를 구성 하는 DNS 이름이 있어야 하 고 어느 toohello NIC VM 또는 tooa 부하 분산 장치에 바인딩할 수 있습니다.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>외부 끝점 추가

트래픽 관리자 외부 끝점 toodirect 트래픽 tooservices Azure 외부에서 호스팅된 사용 하 여 합니다. Azure 끝점과 마찬가지로 외부 끝점은 `Add-AzureRmTrafficManagerEndpointConfig` 뒤 이어 `Set-AzureRmTrafficManagerProfile` 또는 `New-AzureRMTrafficManagerEndpoint`을 사용하여 추가할 수 있습니다.

외부 끝점을 지정하는 경우:

* hello 'Target' 매개 변수를 사용 하 여 hello 끝점 도메인 이름을 지정 해야 합니다.
* Hello 'Performance' 트래픽 라우팅 메서드를 사용 하는 경우에 hello 'EndpointLocation'가 필요 합니다. 그렇지 않은 경우 선택적입니다. hello 값 이어야 합니다는 [올바른 Azure 지역 이름](https://azure.microsoft.com/regions/)합니다.
* hello '가중치' 및 'Priority'는 선택 사항입니다.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>예시 1: `Add-AzureRmTrafficManagerEndpointConfig`과 `Set-AzureRmTrafficManagerProfile`를 사용하여 외부 끝점 추가

이 예에서 만든 트래픽 관리자 프로필, 두 개의 외부 끝점을 추가 하 hello 변경 내용을 커밋합니다.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>예시 2: `New-AzureRmTrafficManagerEndpoint`을 사용하여 외부 끝점 추가

이 예제에서는 외부 끝점 tooan 기존 프로필을 추가합니다. hello 프로필 및 리소스 그룹 이름을 사용 하 여 hello 프로필을 지정 합니다.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>'중첩' 끝점 추가

각 트래픽 관리자 프로필은 단일 트래픽 라우팅 방법을 지정합니다. 그러나 단일 트래픽 관리자 프로필에서 제공 hello 라우팅 보다 더 정교한 트래픽 라우팅이 필요로 하는 시나리오가 있습니다. 둘 이상의 트래픽 라우팅 방법의 트래픽 관리자 프로필 toocombine hello 혜택을 중첩할 수 있습니다. 중첩 된 프로필을 사용 하면 더 큰 toooverride hello 기본 트래픽 관리자 동작 toosupport 및 더 복잡 한 응용 프로그램 배포. 자세한 예시는 [중첩 Traffic Manager 프로필](traffic-manager-nested-profiles.md)을 참조하세요.

중첩 된 끝점 hello 부모 프로필을 특정 끝점 형식 'NestedEndpoints'를 사용 하 여 구성 되었습니다. 중첩된 끝점을 지정하는 경우:

* hello 'targetResourceId' 매개 변수를 사용 하 여 hello 끝점을 지정 해야 합니다.
* Hello 'Performance' 트래픽 라우팅 메서드를 사용 하는 경우에 hello 'EndpointLocation'가 필요 합니다. 그렇지 않은 경우 선택적입니다. hello 값 이어야 합니다는 [올바른 Azure 지역 이름](http://azure.microsoft.com/regions/)합니다.
* '가중치' hello 되며 'Priority' Azure 끝점의 경우와 선택 사항입니다.
* hello 'MinChildEndpoints' 매개 변수는 선택 사항입니다. hello 기본값은 '1'입니다. 사용 가능한 끝점 수가 hello이이 임계값에 미달할 hello 자식 프로필 '저하' 및 트래픽 toohello hello 부모 프로필의 다른 끝점으로 넘깁니다 hello 부모 프로필 고려 합니다.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>예시 1: `Add-AzureRmTrafficManagerEndpointConfig`과 `Set-AzureRmTrafficManagerProfile`를 사용하여 중첩 끝점 추가

이 예에서 만든 새로운 트래픽 관리자 자식 및 부모 프로필, 중첩된 끝점 toohello 부모로 hello 하위 항목 추가 하 hello 변경 내용을 커밋합니다.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

이 예에서는 간단한 설명을 위해 우리는 다른 끝점 toohello 자식 또는 부모 프로필 추가 하지 않았습니다.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>예시 2: `New-AzureRmTrafficManagerEndpoint`을 사용하여 중첩 끝점 추가

이 예제에서는 중첩 된 끝점 tooan 기존 부모 프로필 기존 자식 프로필을 추가합니다. hello 프로필 및 리소스 그룹 이름을 사용 하 여 hello 프로필을 지정 합니다.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Traffic Manager 끝점 업데이트

기존 트래픽 관리자 끝점은 두 가지 방법으로 tooupdate:

1. 사용 하 여 hello 트래픽 관리자 프로필 가져오기 `Get-AzureRmTrafficManagerProfile`, hello 프로필 내 hello 끝점 속성을 업데이트 하 고 사용 하 여 hello 변경 내용 커밋 `Set-AzureRmTrafficManagerProfile`합니다. 이 메서드는 한 번에 둘 이상의 끝점 수 tooupdate는 hello 장점이.
2. 사용 하 여 hello 트래픽 관리자 끝점 가져오기 `Get-AzureRmTrafficManagerEndpoint`, hello 끝점 속성을 업데이트 하 고 사용 하 여 hello 변경 내용 커밋 `Set-AzureRmTrafficManagerEndpoint`합니다. 이 메서드는 hello 프로필에서 끝점 배열 hello에 대 한 인덱싱이 필요 하지 않습니다 때문에 더 간단 합니다.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>예시 1: `Get-AzureRmTrafficManagerProfile`과 `Set-AzureRmTrafficManagerProfile`를 사용하여 끝점 업데이트

이 예제에서는 기존 프로필 내에서 두 개의 끝점에서 hello 우선 순위를 수정 합니다.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>예시 2: `Get-AzureRmTrafficManagerEndpoint`과 `Set-AzureRmTrafficManagerEndpoint`를 사용하여 끝점 업데이트

이 예제에서는 기존 프로필에 있는 단일 끝점의 hello 가중치를 수정 합니다.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>끝점 및 프로필 활성화 및 비활성화

트래픽 관리자를 사용 하도록 설정 및 해제, 설정 및 해제의 전체 프로필을 만들 수 있으며 개별 끝점 toobe를 사용 합니다.
가져오기/업데이트/설정 hello 끝점 또는 프로필 리소스에서 변경할 수 있습니다. toostreamline 이러한 일반적인 작업에도 전용된 cmdlet을 통해 지원 됩니다.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>예제 1: Traffic Manager 프로필 활성화 및 비활성화

tooenable 트래픽 관리자 프로필을 사용 하 여 `Enable-AzureRmTrafficManagerProfile`합니다. hello 프로필은 프로필 개체를 사용 하 여 지정할 수 있습니다. hello 프로필 개체 또는 전달할 수 있습니다 hello 파이프라인을 통해 hello를 사용 하 여 '-TrafficManagerProfile' 매개 변수입니다. 이 예제에서는 hello 프로필 hello 프로필 및 리소스 그룹 이름으로 지정 합니다.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

트래픽 관리자 프로필 toodisable:

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

hello 사용 안 함 AzureRmTrafficManagerProfile cmdlet 확인 메시지를 표시 합니다. Hello를 사용 하 여이 프롬프트를 보류 될 수 있습니다 '-Force' 매개 변수입니다.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>예제 2: Traffic Manager 끝점 활성화 및 비활성화

tooenable 트래픽 관리자 끝점을 사용 하 여 `Enable-AzureRmTrafficManagerEndpoint`합니다. 두 가지 방법으로 toospecify hello 끝점

1. Hello 또는 hello 파이프라인을 통해 전달 되는 TrafficManagerEndpoint 개체를 사용 하 여 '-TrafficManagerEndpoint' 매개 변수
2. Hello 끝점 이름, 끝점 유형, 프로필 이름 및 리소스 그룹 이름을 사용 하 여:

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

마찬가지로, toodisable 트래픽 관리자 끝점:

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

와 마찬가지로 `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet 확인 메시지를 표시 합니다. Hello를 사용 하 여이 프롬프트를 보류 될 수 있습니다 '-Force' 매개 변수입니다.

## <a name="delete-a-traffic-manager-endpoint"></a>Traffic Manager 끝점 삭제

tooremove 개별 끝점을 사용 하 여 hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

이 cmdlet은 확인 프롬프트를 표시합니다. Hello를 사용 하 여이 프롬프트를 보류 될 수 있습니다 '-Force' 매개 변수입니다.

## <a name="delete-a-traffic-manager-profile"></a>Traffic Manager 프로필 삭제

toodelete 트래픽 관리자 프로필을 사용 하 여 hello `Remove-AzureRmTrafficManagerProfile` hello 프로필 및 리소스 그룹 이름을 지정 하는 cmdlet:

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

이 cmdlet은 확인 프롬프트를 표시합니다. Hello를 사용 하 여이 프롬프트를 보류 될 수 있습니다 '-Force' 매개 변수입니다.

삭제 하는 hello 프로필 toobe 프로필 개체를 사용 하 여 지정할 수 있습니다.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

이 순서는 파이프될 수도 있습니다.

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>다음 단계

[Traffic Manager 모니터링](traffic-manager-monitoring.md)

[Traffic Manager 성능 고려 사항](traffic-manager-performance-considerations.md)
