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
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="7e743-103">Azure Network Watcher를 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7e743-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7e743-104">포털</span><span class="sxs-lookup"><span data-stu-id="7e743-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="7e743-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e743-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="7e743-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7e743-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="7e743-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7e743-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="7e743-108">REST API</span><span class="sxs-lookup"><span data-stu-id="7e743-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="7e743-109">네트워크 감시자 toounderstanding Azure의 네트워크 리소스 관련해 서 다양 한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="7e743-110">이러한 기능 중 하나는 리소스 문제 해결입니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="7e743-111">리소스 문제를 해결 하는 hello 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="7e743-112">호출 되 면 네트워크 감시자 가상 네트워크 게이트웨이 또는 연결의 hello 상태를 검사 하 고 해당 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="7e743-113">이 문서는 현재 리소스 문제 해결을 위해 사용할 수 있는 hello 다른 관리 작업을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="7e743-114">**Virtual Network 게이트웨이 문제 해결**</span><span class="sxs-lookup"><span data-stu-id="7e743-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="7e743-115">**연결 문제 해결**</span><span class="sxs-lookup"><span data-stu-id="7e743-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="7e743-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="7e743-116">Before you begin</span></span>

<span data-ttu-id="7e743-117">ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="7e743-118">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="7e743-119">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="7e743-120">지원되는 게이트웨이 유형 목록을 보려면 [지원되는 게이트웨이 유형](network-watcher-troubleshoot-overview.md#supported-gateway-types)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="7e743-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="7e743-121">개요</span><span class="sxs-lookup"><span data-stu-id="7e743-121">Overview</span></span>

<span data-ttu-id="7e743-122">Hello 기능을 제공 네트워크 감시자 문제 해결 가상 네트워크 게이트웨이 및 연결 때 발생 하는 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="7e743-123">요청을 만들 때 toohello 리소스 문제 해결, 로그 쿼리 고 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="7e743-124">검사 완료 되 면 hello 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="7e743-125">hello 해결 API 요청은 오래 실행 중인 요청 여러 분 tooreturn 결과 소요 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="7e743-126">로그는 저장소 계정의 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="7e743-127">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="7e743-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="7e743-128">Virtual Network 게이트웨이 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7e743-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="7e743-129">POST hello 요청 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7e743-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="7e743-130">다음 예제에서는 가상 네트워크 게이트웨이의 hello 상태를 쿼리 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="7e743-131">하므로이 작업은 오래 hello 작업을 쿼리 하기 위한 URI hello 실행 되 고 hello 응답 다음 그림과 같이 hello 결과 대 한 URI hello hello 응답 헤더에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="7e743-132">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="7e743-132">**Important Values**</span></span>

* <span data-ttu-id="7e743-133">**Azure AsyncOperation** -이 속성에 포함 hello URI tooquery hello 비동기 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7e743-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="7e743-134">**위치** -hello hello 결과가 있는 경우 hello 작업이 완료 되는 URI가 포함 되어이 속성</span><span class="sxs-lookup"><span data-stu-id="7e743-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="7e743-135">쿼리 완료에 대 한 hello 비동기 작업</span><span class="sxs-lookup"><span data-stu-id="7e743-135">Query hello async operation for completion</span></span>

<span data-ttu-id="7e743-136">Hello 다음 예제와 같이 hello 작업의 진행 상황 hello에 대 한 작업 URI tooquery hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="7e743-137">Hello 작업이 진행 중에서 상태인 동안 hello 응답 표시 **InProgress** hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="7e743-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="7e743-138">Hello 작업 완료 hello 상태가 변경 될 경우 너무**Succeeded**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="7e743-139">Hello 결과 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-139">Retrieve hello results</span></span>

<span data-ttu-id="7e743-140">Hello 상태 반환 되 면 **Succeeded**, hello 결과 hello operationResult URI tooretrieve에서 GET 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="7e743-141">hello 다음 응답은 게이트웨이 문제 해결의 hello 결과 쿼리할 때 반환 일반적으로 성능이 저하 된 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="7e743-142">참조 [hello 결과 이해](#understanding-the-results) tooget hello 응답 평균에서 어떤 hello 속성에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

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


## <a name="troubleshoot-connections"></a><span data-ttu-id="7e743-143">연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7e743-143">Troubleshoot Connections</span></span>

<span data-ttu-id="7e743-144">다음 예제는 연결의 hello 상태를 쿼리 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-144">hello following example queries hello status of a Connection.</span></span>

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
> <span data-ttu-id="7e743-145">hello 작업 문제 해결에 대 한 연결 및 해당 게이트웨이 병렬로 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="7e743-146">hello 작업 이전 toorunning 완료 되어야 하며 hello 이전 리소스에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="7e743-147">이 hello 응답 헤더에 장기 실행 트랜잭션이 hello 작업과 hello 결과 대 한 URI hello를 쿼리 하기 위한 URI hello hello 응답 뒤에 표시 된 대로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="7e743-148">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="7e743-148">**Important Values**</span></span>

* <span data-ttu-id="7e743-149">**Azure AsyncOperation** -이 속성에 포함 hello URI tooquery hello 비동기 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7e743-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="7e743-150">**위치** -hello hello 결과가 있는 경우 hello 작업이 완료 되는 URI가 포함 되어이 속성</span><span class="sxs-lookup"><span data-stu-id="7e743-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="7e743-151">쿼리 완료에 대 한 hello 비동기 작업</span><span class="sxs-lookup"><span data-stu-id="7e743-151">Query hello async operation for completion</span></span>

<span data-ttu-id="7e743-152">Hello 다음 예제와 같이 hello 작업의 진행 상황 hello에 대 한 작업 URI tooquery hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="7e743-153">Hello 작업이 진행 중에서 상태인 동안 hello 응답 표시 **InProgress** hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="7e743-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="7e743-154">Hello 작업이 완료 되 면 hello 상태 변경 너무**Succeeded**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="7e743-155">hello 다음 응답은 일반적으로 hello 결과 쿼리는 연결 문제를 해결 하는 경우 반환 된 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="7e743-156">Hello 결과 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-156">Retrieve hello results</span></span>

<span data-ttu-id="7e743-157">Hello 상태 반환 되 면 **Succeeded**, hello 결과 hello operationResult URI tooretrieve에서 GET 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="7e743-158">hello 다음 응답은 일반적으로 hello 결과 쿼리는 연결 문제를 해결 하는 경우 반환 된 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

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

## <a name="understanding-hello-results"></a><span data-ttu-id="7e743-159">Hello 결과 이해</span><span class="sxs-lookup"><span data-stu-id="7e743-159">Understanding hello results</span></span>

<span data-ttu-id="7e743-160">hello 동작 텍스트 tooresolve 문제 hello 하는 방법에 대 한 일반적인 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="7e743-161">Hello 문제에 대 한 작업을 수행할 수, 링크를 추가 하는 지침과 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="7e743-162">Hello 경우에서 hello 응답을 자세한 지침은 없으며가 있는 hello url tooopen 지원 사례를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="7e743-163">Hello 응답 및 포함 된 항목의 hello 속성에 대 한 자세한 내용은 방문 [네트워크 감시자 문제 해결 개요](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7e743-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="7e743-164">Azure 저장소 계정에서 파일을 다운로드 하는 방법은 참조 너무[.NET을 사용 하 여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="7e743-165">사용할 수 있는 다른 도구는 저장소 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="7e743-166">저장소 탐색기에 대 한 자세한 내용은 여기에 있습니다 링크 hello: [저장소 탐색기](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="7e743-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e743-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e743-167">Next steps</span></span>

<span data-ttu-id="7e743-168">해당 중지 VPN 연결 설정이 변경 되었으며, 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack 아래로 hello 네트워크 보안 그룹 및 보안 규칙을 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e743-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
