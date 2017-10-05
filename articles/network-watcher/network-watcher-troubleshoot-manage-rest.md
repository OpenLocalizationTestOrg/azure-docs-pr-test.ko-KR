---
title: "Azure Network Watcher를 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결 - REST | Microsoft Docs"
description: "REST를 사용하여 Azure Network Watcher에서 Virtual Network 게이트웨이 및 연결 문제를 해결하는 방법을 설명합니다."
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
ms.openlocfilehash: bc61be74d85a309c158716460b918baaf4fa94dc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="580bd-103">Azure Network Watcher를 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="580bd-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="580bd-104">포털</span><span class="sxs-lookup"><span data-stu-id="580bd-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="580bd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="580bd-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="580bd-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="580bd-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="580bd-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="580bd-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="580bd-108">REST API</span><span class="sxs-lookup"><span data-stu-id="580bd-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="580bd-109">Network Watcher는 Azure에서 네트워크 리소스를 이해하는 데 관련된 다양한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="580bd-110">이러한 기능 중 하나는 리소스 문제 해결입니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="580bd-111">리소스 문제 해결은 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="580bd-112">Network Watcher가 호출되면 Virtual Network 게이트웨이 또는 연결의 상태를 검사하거나 해당 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="580bd-113">이 문서에서는 리소스 문제 해결을 위해 현재 사용할 수 있는 여러 관리 태스크를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-113">This article takes you through the different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="580bd-114">**Virtual Network 게이트웨이 문제 해결**</span><span class="sxs-lookup"><span data-stu-id="580bd-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="580bd-115">**연결 문제 해결**</span><span class="sxs-lookup"><span data-stu-id="580bd-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="580bd-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="580bd-116">Before you begin</span></span>

<span data-ttu-id="580bd-117">PowerShell을 사용하여 REST API를 호출하는 데 ARMclient가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-117">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="580bd-118">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="580bd-119">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-119">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="580bd-120">지원되는 게이트웨이 유형 목록을 보려면 [지원되는 게이트웨이 유형](network-watcher-troubleshoot-overview.md#supported-gateway-types)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="580bd-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="580bd-121">개요</span><span class="sxs-lookup"><span data-stu-id="580bd-121">Overview</span></span>

<span data-ttu-id="580bd-122">Network Watcher 문제 해결은 Virtual Network 게이트웨이 및 연결에 발생한 문제를 해결하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-122">Network Watcher troubleshooting provides the ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="580bd-123">리소스 문제 해결을 요청하는 경우 로그를 쿼리하고 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-123">When a request is made to the resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="580bd-124">검사가 완료되면 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-124">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="580bd-125">문제 해결 API 요청은 장기 실행 요청이며 결과를 반환하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-125">The troubleshoot API requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="580bd-126">로그는 저장소 계정의 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="580bd-127">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="580bd-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="580bd-128">Virtual Network 게이트웨이 문제 해결</span><span class="sxs-lookup"><span data-stu-id="580bd-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-the-troubleshoot-request"></a><span data-ttu-id="580bd-129">문제 해결 요청 게시</span><span class="sxs-lookup"><span data-stu-id="580bd-129">POST the troubleshoot request</span></span>

<span data-ttu-id="580bd-130">다음 예제는 Virtual Network 게이트웨이의 상태를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-130">The following example queries the status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="580bd-131">이 작업은 장시간 실행되므로 작업 쿼리를 위한 URI와 결과에 대한 URI가 다음 응답에 표시된 것처럼 응답 헤더에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-131">Since this operation is long running, the URI for querying the operation and the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="580bd-132">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="580bd-132">**Important Values**</span></span>

* <span data-ttu-id="580bd-133">**Azure-AsyncOperation** - 이 속성에는 동기화 문제 해결 작업을 쿼리할 URI가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-133">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="580bd-134">**위치** - 이 속성에는 작업이 완료될 때 결과가 있는 URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-134">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="580bd-135">동기화 작업의 완료 쿼리</span><span class="sxs-lookup"><span data-stu-id="580bd-135">Query the async operation for completion</span></span>

<span data-ttu-id="580bd-136">다음 예제에서 볼 수 있듯이 작업 URI를 사용하여 작업 진행 상태를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-136">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="580bd-137">작업이 진행 중인 동안에는 다음 예제에서 볼 수 있듯이 응답에 **진행 중**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-137">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="580bd-138">작업이 완료되면 상태가 **성공**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-138">When the operation is complete the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-the-results"></a><span data-ttu-id="580bd-139">결과 검색</span><span class="sxs-lookup"><span data-stu-id="580bd-139">Retrieve the results</span></span>

<span data-ttu-id="580bd-140">반환된 상태가 **성공**이면 operationResult URI에서 GET 메서드를 호출하여 결과를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-140">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="580bd-141">다음 응답은 게이트웨이 문제 해결 결과를 쿼리할 때 반환된 일반적인 성능 저하 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-141">The following responses are examples of a typical degraded response returned when querying the results of troubleshooting a gateway.</span></span> <span data-ttu-id="580bd-142">응답에서 속성이 의미하는 바를 확실히 알려면 [결과 이해](#understanding-the-results)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="580bd-142">See [Understanding the results](#understanding-the-results) to get clarification on what the properties in the response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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


## <a name="troubleshoot-connections"></a><span data-ttu-id="580bd-143">연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="580bd-143">Troubleshoot Connections</span></span>

<span data-ttu-id="580bd-144">다음 예제는 연결의 상태를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-144">The following example queries the status of a Connection.</span></span>

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
> <span data-ttu-id="580bd-145">문제 해결 작업을 연결 및 해당 게이트웨이에서 병렬로 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-145">The troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="580bd-146">이전 리소스에서 실행하기 전에 작업을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-146">The operation must complete prior to running it on the previous resource.</span></span>

<span data-ttu-id="580bd-147">장시간 실행되는 트랜잭션이므로 응답 헤더에서, 작업 쿼리를 위한 URI와 결과에 대한 URI가 다음 응답에 표시된 것처럼 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-147">Since this is a long running transaction, in the response header, the URI for querying the operation and the URI for the result is returned as shown in the following response:</span></span>

<span data-ttu-id="580bd-148">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="580bd-148">**Important Values**</span></span>

* <span data-ttu-id="580bd-149">**Azure-AsyncOperation** - 이 속성에는 동기화 문제 해결 작업을 쿼리할 URI가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-149">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="580bd-150">**위치** - 이 속성에는 작업이 완료될 때 결과가 있는 URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-150">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="580bd-151">동기화 작업의 완료 쿼리</span><span class="sxs-lookup"><span data-stu-id="580bd-151">Query the async operation for completion</span></span>

<span data-ttu-id="580bd-152">다음 예제에서 볼 수 있듯이 작업 URI를 사용하여 작업 진행 상태를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-152">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="580bd-153">작업이 진행 중인 동안에는 다음 예제에서 볼 수 있듯이 응답에 **진행 중**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-153">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="580bd-154">작업이 완료되면 상태가 **성공**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-154">When the operation is complete, the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="580bd-155">다음 응답은 연결 문제 해결 결과를 쿼리할 때 반환된 일반적인 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-155">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

### <a name="retrieve-the-results"></a><span data-ttu-id="580bd-156">결과 검색</span><span class="sxs-lookup"><span data-stu-id="580bd-156">Retrieve the results</span></span>

<span data-ttu-id="580bd-157">반환된 상태가 **성공**이면 operationResult URI에서 GET 메서드를 호출하여 결과를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-157">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="580bd-158">다음 응답은 연결 문제 해결 결과를 쿼리할 때 반환된 일반적인 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-158">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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

## <a name="understanding-the-results"></a><span data-ttu-id="580bd-159">결과 이해</span><span class="sxs-lookup"><span data-stu-id="580bd-159">Understanding the results</span></span>

<span data-ttu-id="580bd-160">작업 텍스트에서는 문제를 해결하는 방법에 대한 일반적인 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-160">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="580bd-161">문제에 대한 조치를 취할 수 있는 경우 링크는 추가 설명서와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-161">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="580bd-162">추가 지침이 없는 경우에 응답은 지원 사례를 열 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-162">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="580bd-163">응답의 속성 및 포함된 항목에 대한 자세한 내용은 [Network Watcher 문제 해결 개요](network-watcher-troubleshoot-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="580bd-163">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="580bd-164">Azure Storage 계정에서 파일을 다운로드하는 방법에 대한 지침은 [.NET을 사용하여 Azure Blob Storage 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="580bd-164">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="580bd-165">사용할 수 있는 다른 도구는 저장소 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="580bd-166">저장소 탐색기에 대한 자세한 내용은 여기에 있는 [저장소 탐색기](http://storageexplorer.com/) 링크에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-166">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="580bd-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="580bd-167">Next steps</span></span>

<span data-ttu-id="580bd-168">VPN 연결을 중지하도록 설정이 변경된 경우 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md)를 참조하여 문제가 될 수 있는 네트워크 보안 그룹 및 보안 규칙을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="580bd-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
