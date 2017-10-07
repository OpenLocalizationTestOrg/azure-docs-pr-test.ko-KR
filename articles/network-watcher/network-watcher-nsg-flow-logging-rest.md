---
title: "Azure 네트워크 감시자-REST API를 사용 하 여 기록 네트워크 보안 그룹 흐름 aaaManage | Microsoft Docs"
description: "이 페이지에서는 toomanage 네트워크 보안 그룹 흐름 REST API와 Azure 네트워크 감시자 로그인 하는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a>REST API를 사용하여 네트워크 보안 그룹 흐름 로그 구성

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 IP 트래픽 ingress 및 egress에 대 한 tooview 정보 수 있는 네트워크 감시자의 기능입니다. 이러한 흐름 로그 json 형식으로 작성 되 고 아웃 바운드 표시 및 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜)에 대 한 5-튜플 정보에 각 규칙 별로 인바운드 흐름 hello NIC hello 흐름 적용 하 고 트래픽이 허용 된 경우 hello 또는 거부 됩니다.

## <a name="before-you-begin"></a>시작하기 전에

ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다. ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.

> [!Important]
> 네트워크 감시자 REST API에 대 한 호출 hello hello 요청 URI는 hello 진단 작업에서 수행 하는 hello 리소스가 아닌 hello 네트워크 감시자를 포함 하는 hello 리소스 그룹에에서 리소스 그룹 이름입니다.

## <a name="scenario"></a>시나리오

이 문서에서 다루는 hello 시나리오 tooenable, 사용 안 함, 및 쿼리 hello REST API를 사용 하 여 로그의 흐름 방식 보여 줍니다. 네트워크 보안 그룹 흐름 loggings에 대 한 자세한 toolearn 방문 [네트워크 보안 그룹 흐름 로깅-개요](network-watcher-nsg-flow-logging-overview.md)합니다.

이 시나리오에서는 다음을 수행합니다.

* 흐름 로그를 사용하도록 설정
* 흐름 로그를 사용하지 않도록 설정
* 흐름 로그 상태 쿼리

## <a name="log-in-with-armclient"></a>ARMClient에 로그인

Tooarmclient Azure 자격 증명으로 로그인 합니다.

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a>Insights 공급자 등록

흐름에 대 한 순서 대로 로깅 toowork 성공적으로 hello **Microsoft.Insights** 공급자를 등록 해야 합니다. 경우 hello 확실 하지 않은 경우 **Microsoft.Insights** 공급자가 등록 된, 실행 hello 다음 스크립트입니다.

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a>네트워크 보안 그룹 흐름 로그 사용

다음 예제는 hello hello 명령 tooenable 흐름 로그를 보여 줍니다.

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

hello에서 응답이 반환 되었습니다 hello 위의 예는 다음과 같습니다.

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a>네트워크 보안 그룹 흐름 로그를 사용하지 않도록 설정

다음 예에서는 toodisable 흐름 사용 하 여 hello를 기록 합니다. hello 호출은 제외 하 고 흐름 로그를 활성화할 때와 동일한 hello **false** 사용 하도록 설정 하는 hello 속성에 설정 되어 있습니다.

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

hello에서 응답이 반환 되었습니다 hello 위의 예는 다음과 같습니다.

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a>흐름 로그 쿼리

쿼리 hello 흐름의 상태는 REST 호출 다음 hello를 네트워크 보안 그룹에 기록 합니다.

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

hello 다음은 반환 하는 hello 응답의 예입니다.

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a>흐름 로그 다운로드

흐름 로그의 hello 저장소 위치를 만들 때 정의 됩니다. 이러한 흐름 저장 된 로그 tooa 저장소 계정이 여기에서 다운로드할 수 있는 Microsoft Azure 저장소 탐색기는 편리한 도구 tooaccess: http://storageexplorer.com/

저장소 계정이 지정 되어 있으면 hello 수정할 수 있는 위치에서 저장소 계정은 tooa 패킷 캡처 파일에 저장 됩니다.

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a>다음 단계

너무 방법에 대해 알아봅니다[PowerBI와 NSG 흐름 로그를 시각화 합니다.](network-watcher-visualize-nsg-flow-logs-power-bi.md)

너무 방법에 대해 알아봅니다[오픈 소스 도구와 함께 NSG 흐름 로그를 시각화 합니다.](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
