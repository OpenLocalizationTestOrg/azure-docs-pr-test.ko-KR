---
title: "Azure Network Watcher를 사용하여 네트워크 보안 그룹 흐름 로그 관리 - REST API | Microsoft Docs"
description: "이 페이지에서는 REST API를 사용하여 Azure Network Watcher의 네트워크 보안 그룹 흐름 로그를 관리하는 방법을 설명합니다."
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
ms.openlocfilehash: c89a2ab4c39978771c940a819493b4e2283d5f9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="75917-103">REST API를 사용하여 네트워크 보안 그룹 흐름 로그 구성</span><span class="sxs-lookup"><span data-stu-id="75917-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="75917-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="75917-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="75917-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="75917-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="75917-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="75917-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="75917-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="75917-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="75917-108">REST API</span><span class="sxs-lookup"><span data-stu-id="75917-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="75917-109">네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 수신 및 송신 IP 트래픽에 대한 정보를 볼 수 있는 Network Watcher의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="75917-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="75917-110">이러한 흐름 로그는 json 형식으로 작성되고 트래픽이 허용되거나 거부된 경우 각 규칙을 기준으로 아웃바운드 및 인바운드 흐름, 흐름이 적용되는 NIC, 흐름에 대한 5개의 튜플 정보(원본/대상 IP, 원본/대상 포트, 프로토콜)를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75917-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="75917-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="75917-111">Before you begin</span></span>

<span data-ttu-id="75917-112">PowerShell을 사용하여 REST API를 호출하는 데 ARMclient가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75917-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="75917-113">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75917-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="75917-114">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="75917-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="75917-115">Network Watcher REST API 호출의 경우 요청 URI에 있는 리소스 그룹 이름은 진단 작업이 수행되는 리소스가 아니라, Network Watcher를 포함하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="75917-115">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="75917-116">시나리오</span><span class="sxs-lookup"><span data-stu-id="75917-116">Scenario</span></span>

<span data-ttu-id="75917-117">이 문서에서 다루는 시나리오는 REST API를 사용하여 흐름 로그를 사용하거나 사용하지 않도록 설정하고 쿼리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75917-117">The scenario covered in this article shows you how to enable, disable, and query flow logs using the REST API.</span></span> <span data-ttu-id="75917-118">네트워크 보안 그룹 흐름 로깅에 대한 자세한 내용은 [네트워크 보안 그룹 흐름 로깅 - 개요](network-watcher-nsg-flow-logging-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75917-118">To learn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="75917-119">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="75917-119">In this scenario, you will:</span></span>

* <span data-ttu-id="75917-120">흐름 로그를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="75917-120">Enable flow logs</span></span>
* <span data-ttu-id="75917-121">흐름 로그를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="75917-121">Disable flow logs</span></span>
* <span data-ttu-id="75917-122">흐름 로그 상태 쿼리</span><span class="sxs-lookup"><span data-stu-id="75917-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="75917-123">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="75917-123">Log in with ARMClient</span></span>

<span data-ttu-id="75917-124">Azure 자격 증명으로 armclient에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="75917-124">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="75917-125">Insights 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="75917-125">Register Insights provider</span></span>

<span data-ttu-id="75917-126">흐름 로깅이 성공적으로 작동하기 위해서 **Microsoft.Insights** 공급자를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75917-126">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="75917-127">**Microsoft.Insights** 공급자가 등록되어 있는지 확실하지 않은 경우 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="75917-127">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="75917-128">네트워크 보안 그룹 흐름 로그 사용</span><span class="sxs-lookup"><span data-stu-id="75917-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="75917-129">다음 예제에서는 흐름 로그를 사용하도록 설정하는 명령이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75917-129">The command to enable flow logs is shown in the following example:</span></span>

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

<span data-ttu-id="75917-130">이전 예제에서 반환한 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75917-130">The response returned from the preceding example is as follows:</span></span>

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

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="75917-131">네트워크 보안 그룹 흐름 로그를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="75917-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="75917-132">다음 예제를 사용하여 흐름 로그를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75917-132">Use the following example to disable flow logs.</span></span> <span data-ttu-id="75917-133">호출은 흐름 로그를 사용하도록 설정하는 것과 같습니다(단, 활성화된 속성에 대해 **false**가 설정된 경우 제외).</span><span class="sxs-lookup"><span data-stu-id="75917-133">The call is the same as enabling flow logs, except **false** is set for the enabled property.</span></span>

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

<span data-ttu-id="75917-134">이전 예제에서 반환한 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75917-134">The response returned from the preceding example is as follows:</span></span>

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

## <a name="query-flow-logs"></a><span data-ttu-id="75917-135">흐름 로그 쿼리</span><span class="sxs-lookup"><span data-stu-id="75917-135">Query flow logs</span></span>

<span data-ttu-id="75917-136">다음 REST 호출은 네트워크 보안 그룹에서 흐름 로그의 상태를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="75917-136">The following REST call queries the status of flow logs on a Network Security Group.</span></span>

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

<span data-ttu-id="75917-137">다음은 반환된 응답의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="75917-137">The following is an example of the response returned:</span></span>

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

## <a name="download-a-flow-log"></a><span data-ttu-id="75917-138">흐름 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="75917-138">Download a flow log</span></span>

<span data-ttu-id="75917-139">흐름 로그의 저장소 위치를 만들 때 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="75917-139">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="75917-140">저장소 계정에 저장되는 이러한 흐름 로그에 액세스하는 편리한 도구는 Microsoft Azure Storage 탐색기이며 http://storageexplorer.com/에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75917-140">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="75917-141">저장소 계정이 지정되어 있으면 패킷 캡처 파일은 다음 위치에서 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="75917-141">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="75917-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75917-142">Next steps</span></span>

<span data-ttu-id="75917-143">[PowerBI를 사용하여 NSG 흐름 로그를 시각화](network-watcher-visualize-nsg-flow-logs-power-bi.md)하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="75917-143">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="75917-144">[오픈 소스 도구를 사용하여 NSG 흐름 로그를 시각화](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="75917-144">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
