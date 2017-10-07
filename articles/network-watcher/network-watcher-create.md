---
title: "Azure 네트워크 감시자 인스턴스 aaaCreate | Microsoft Docs"
description: "이 페이지에서는 hello 단계 toocreate 네트워크 감시자의 인스턴스 hello 포털 및 Azure REST API를 사용 하 여"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>Azure Network Watcher 인스턴스 만들기

네트워크 감시자는 toomonitor 있습니다 수 있도록 하는 지역 서비스 및 네트워크 시나리오의 수준에서 및 Azure에서 상태를 진단 합니다. 수준 모니터링 시나리오는 최종 tooend 네트워크 수준 보기에서 toodiagnose 문제가 있습니다. 네트워크 문제 진단 및 시각화 도구를 사용할 수 있는 네트워크 감시자 insights tooyour Azure 네트워크에에서 가져오고 이해, 진단, 하는 데 도움이 됩니다.

> [!NOTE]
> 네트워크 감시자는 현재 지원 CLI 1.0, hello 지침 toocreate 새 네트워크 감시자 인스턴스 제공 됩니다 CLI 1.0에 대 한 합니다.

## <a name="create-a-network-watcher-in-hello-portal"></a>네트워크 감시자 hello 포털에서 만들기

너무 이동**더 서비스** > **네트워킹** > **네트워크 감시자**합니다. 네트워크 감시자 tooenable 원하는 모든 hello 구독을 선택할 수 있습니다에 대 한 합니다. 이 작업은 사용할 수 있는 모든 지역에서 Network Watcher를 만듭니다.

![Network Watcher 만들기][1]

네트워크 감시자 hello 포털을 사용 하 여 사용 하도록 설정 하면 hello hello 네트워크 감시자 인스턴스 이름이 자동으로 설정 됩니다 tooNetworkWatcher_region_name region_name toohello hello 인스턴스가 활성화 된 Azure 영역을 해당 하는 위치입니다.  예를 들어 미국 중서부에서 활성화된 Network Watcher의 이름은 NetworkWatcher_westcentralus입니다.

또한 hello 네트워크 감시자 인스턴스 NetworkWatcherRG 라는 리소스 그룹에 자동으로 추가 됩니다.  이 리소스 그룹은 아직 존재하지 않는 경우 만들어집니다.

네트워크 감시자 인스턴스와 hello의 toocustomize hello 이름이 필요한 경우 리소스 그룹에 배치 됩니다, 그리고 아래에서 설명 하는 Powershell, REST API hello 또는 ARMClient 방법을 사용할 수 있습니다.  각 옵션에 hello 네트워크 감시자를 배치 하기 전에 hello 리소스 그룹이 있어야 합니다.  

## <a name="create-a-network-watcher-with-powershell"></a>PowerShell을 사용하여 Network Watcher 만들기

다음 예제는 hello를 실행 하는 네트워크 감시자의 인스턴스 toocreate:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a>네트워크 감시자 hello REST API를 사용 하 여 만들기

ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다. ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.

### <a name="log-in-with-armclient"></a>ARMClient에 로그인

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a>네트워크 감시자 hello 만들기

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a>다음 단계

네트워크 감시자의 인스턴스를가지고 있습니다 사용할 수 있는 hello 기능에 알아봅니다.

* [토폴로지](network-watcher-topology-overview.md)
* [패킷 캡처](network-watcher-packet-capture-overview.md)
* [IP 흐름 확인](network-watcher-ip-flow-verify-overview.md)
* [다음 홉](network-watcher-next-hop-overview.md)
* [보안 그룹 보기](network-watcher-security-group-view-overview.md)
* [NSG 흐름 로깅](network-watcher-nsg-flow-logging-overview.md)
* [Virtual Network 게이트웨이 문제 해결](network-watcher-troubleshoot-overview.md)

네트워크 감시자 인스턴스를 만든 후 다음 hello 문서가 패키지 캡처를 구성할 수 있습니다: [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)

[1]: ./media/network-watcher-create/figure1.png











