---
title: "aaaTroubleshoot 가상 네트워크 게이트웨이 및 연결 사용 Azure 네트워크 감시자-REST | Microsoft Docs"
description: "이 페이지에서는 REST을 tootroubleshoot 가상 네트워크 게이트웨이 및 Azure 네트워크 감시자를 사용 하 여 연결 하는 방법을 설명합니다"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a>Azure Network Watcher를 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결

> [!div class="op_single_selector"]
> - [포털](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

네트워크 감시자 toounderstanding Azure의 네트워크 리소스 관련해 서 다양 한 기능을 제공 합니다. 이러한 기능 중 하나는 리소스 문제 해결입니다. 리소스 문제를 해결 하는 hello 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다. 호출 되 면 네트워크 감시자 가상 네트워크 게이트웨이 또는 연결의 hello 상태를 검사 하 고 해당 결과 반환 합니다.

이 문서는 현재 리소스 문제 해결을 위해 사용할 수 있는 hello 다른 관리 작업을 안내 합니다.

- [**Virtual Network 게이트웨이 문제 해결**](#troubleshoot-a-virtual-network-gateway)
- [**연결 문제 해결**](#troubleshoot-connections)

## <a name="before-you-begin"></a>시작하기 전에

ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다. ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.

지원되는 게이트웨이 유형 목록을 보려면 [지원되는 게이트웨이 유형](network-watcher-troubleshoot-overview.md#supported-gateway-types)을 방문하세요.

## <a name="overview"></a>개요

Hello 기능을 제공 네트워크 감시자 문제 해결 가상 네트워크 게이트웨이 및 연결 때 발생 하는 문제를 해결 합니다. 요청을 만들 때 toohello 리소스 문제 해결, 로그 쿼리 고 검사 합니다. 검사 완료 되 면 hello 결과가 반환 됩니다. hello 해결 API 요청은 오래 실행 중인 요청 여러 분 tooreturn 결과 소요 될 수 있습니다. 로그는 저장소 계정의 컨테이너에 저장됩니다.

## <a name="log-in-with-armclient"></a>ARMClient에 로그인

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a>Virtual Network 게이트웨이 문제 해결


### <a name="post-hello-troubleshoot-request"></a>POST hello 요청 문제 해결

다음 예제에서는 가상 네트워크 게이트웨이의 hello 상태를 쿼리 하는 번호입니다.

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

하므로이 작업은 오래 hello 작업을 쿼리 하기 위한 URI hello 실행 되 고 hello 응답 다음 그림과 같이 hello 결과 대 한 URI hello hello 응답 헤더에 반환 됩니다.

**중요한 값**

* **Azure AsyncOperation** -이 속성에 포함 hello URI tooquery hello 비동기 작업 문제 해결
* **위치** -hello hello 결과가 있는 경우 hello 작업이 완료 되는 URI가 포함 되어이 속성

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a>쿼리 완료에 대 한 hello 비동기 작업

Hello 다음 예제와 같이 hello 작업의 진행 상황 hello에 대 한 작업 URI tooquery hello를 사용 합니다.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Hello 작업이 진행 중에서 상태인 동안 hello 응답 표시 **InProgress** hello 다음 예제와 같이:

```json
{
  "status": "InProgress"
}
```

Hello 작업 완료 hello 상태가 변경 될 경우 너무**Succeeded**합니다.

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a>Hello 결과 검색 합니다.

Hello 상태 반환 되 면 **Succeeded**, hello 결과 hello operationResult URI tooretrieve에서 GET 메서드를 호출 합니다.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

hello 다음 응답은 게이트웨이 문제 해결의 hello 결과 쿼리할 때 반환 일반적으로 성능이 저하 된 응답의 예입니다. 참조 [hello 결과 이해](#understanding-the-results) tooget hello 응답 평균에서 어떤 hello 속성에 대 한 설명입니다.

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a>연결 문제 해결

다음 예제는 연결의 hello 상태를 쿼리 하는 번호입니다.

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> hello 작업 문제 해결에 대 한 연결 및 해당 게이트웨이 병렬로 실행할 수 없습니다. hello 작업 이전 toorunning 완료 되어야 하며 hello 이전 리소스에 해당 합니다.

이 hello 응답 헤더에 장기 실행 트랜잭션이 hello 작업과 hello 결과 대 한 URI hello를 쿼리 하기 위한 URI hello hello 응답 뒤에 표시 된 대로 반환 됩니다.

**중요한 값**

* **Azure AsyncOperation** -이 속성에 포함 hello URI tooquery hello 비동기 작업 문제 해결
* **위치** -hello hello 결과가 있는 경우 hello 작업이 완료 되는 URI가 포함 되어이 속성

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a>쿼리 완료에 대 한 hello 비동기 작업

Hello 다음 예제와 같이 hello 작업의 진행 상황 hello에 대 한 작업 URI tooquery hello를 사용 합니다.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Hello 작업이 진행 중에서 상태인 동안 hello 응답 표시 **InProgress** hello 다음 예제와 같이:

```json
{
  "status": "InProgress"
}
```

Hello 작업이 완료 되 면 hello 상태 변경 너무**Succeeded**합니다.

```json
{
  "status": "Succeeded"
}
```

hello 다음 응답은 일반적으로 hello 결과 쿼리는 연결 문제를 해결 하는 경우 반환 된 응답의 예입니다.

### <a name="retrieve-hello-results"></a>Hello 결과 검색 합니다.

Hello 상태 반환 되 면 **Succeeded**, hello 결과 hello operationResult URI tooretrieve에서 GET 메서드를 호출 합니다.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

hello 다음 응답은 일반적으로 hello 결과 쿼리는 연결 문제를 해결 하는 경우 반환 된 응답의 예입니다.

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a>Hello 결과 이해

hello 동작 텍스트 tooresolve 문제 hello 하는 방법에 대 한 일반적인 지침을 제공 합니다. Hello 문제에 대 한 작업을 수행할 수, 링크를 추가 하는 지침과 함께 제공 됩니다. Hello 경우에서 hello 응답을 자세한 지침은 없으며가 있는 hello url tooopen 지원 사례를 제공 합니다.  Hello 응답 및 포함 된 항목의 hello 속성에 대 한 자세한 내용은 방문 [네트워크 감시자 문제 해결 개요](network-watcher-troubleshoot-overview.md)

Azure 저장소 계정에서 파일을 다운로드 하는 방법은 참조 너무[.NET을 사용 하 여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다. 사용할 수 있는 다른 도구는 저장소 탐색기입니다. 저장소 탐색기에 대 한 자세한 내용은 여기에 있습니다 링크 hello: [저장소 탐색기](http://storageexplorer.com/)

## <a name="next-steps"></a>다음 단계

해당 중지 VPN 연결 설정이 변경 되었으며, 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack 아래로 hello 네트워크 보안 그룹 및 보안 규칙을 문제가 될 수 있습니다.
