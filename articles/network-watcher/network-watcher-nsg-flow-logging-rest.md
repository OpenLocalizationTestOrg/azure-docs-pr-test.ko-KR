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
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="0d584-103">REST API를 사용하여 네트워크 보안 그룹 흐름 로그 구성</span><span class="sxs-lookup"><span data-stu-id="0d584-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0d584-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="0d584-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="0d584-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d584-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="0d584-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0d584-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="0d584-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0d584-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="0d584-108">REST API</span><span class="sxs-lookup"><span data-stu-id="0d584-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="0d584-109">네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 IP 트래픽 ingress 및 egress에 대 한 tooview 정보 수 있는 네트워크 감시자의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="0d584-110">이러한 흐름 로그 json 형식으로 작성 되 고 아웃 바운드 표시 및 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜)에 대 한 5-튜플 정보에 각 규칙 별로 인바운드 흐름 hello NIC hello 흐름 적용 하 고 트래픽이 허용 된 경우 hello 또는 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0d584-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0d584-111">Before you begin</span></span>

<span data-ttu-id="0d584-112">ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="0d584-113">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="0d584-114">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="0d584-115">네트워크 감시자 REST API에 대 한 호출 hello hello 요청 URI는 hello 진단 작업에서 수행 하는 hello 리소스가 아닌 hello 네트워크 감시자를 포함 하는 hello 리소스 그룹에에서 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="0d584-116">시나리오</span><span class="sxs-lookup"><span data-stu-id="0d584-116">Scenario</span></span>

<span data-ttu-id="0d584-117">이 문서에서 다루는 hello 시나리오 tooenable, 사용 안 함, 및 쿼리 hello REST API를 사용 하 여 로그의 흐름 방식 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="0d584-118">네트워크 보안 그룹 흐름 loggings에 대 한 자세한 toolearn 방문 [네트워크 보안 그룹 흐름 로깅-개요](network-watcher-nsg-flow-logging-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="0d584-119">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-119">In this scenario, you will:</span></span>

* <span data-ttu-id="0d584-120">흐름 로그를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="0d584-120">Enable flow logs</span></span>
* <span data-ttu-id="0d584-121">흐름 로그를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="0d584-121">Disable flow logs</span></span>
* <span data-ttu-id="0d584-122">흐름 로그 상태 쿼리</span><span class="sxs-lookup"><span data-stu-id="0d584-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="0d584-123">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="0d584-123">Log in with ARMClient</span></span>

<span data-ttu-id="0d584-124">Tooarmclient Azure 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="0d584-125">Insights 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="0d584-125">Register Insights provider</span></span>

<span data-ttu-id="0d584-126">흐름에 대 한 순서 대로 로깅 toowork 성공적으로 hello **Microsoft.Insights** 공급자를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="0d584-127">경우 hello 확실 하지 않은 경우 **Microsoft.Insights** 공급자가 등록 된, 실행 hello 다음 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="0d584-128">네트워크 보안 그룹 흐름 로그 사용</span><span class="sxs-lookup"><span data-stu-id="0d584-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="0d584-129">다음 예제는 hello hello 명령 tooenable 흐름 로그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-129">hello command tooenable flow logs is shown in hello following example:</span></span>

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

<span data-ttu-id="0d584-130">hello에서 응답이 반환 되었습니다 hello 위의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-130">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="0d584-131">네트워크 보안 그룹 흐름 로그를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="0d584-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="0d584-132">다음 예에서는 toodisable 흐름 사용 하 여 hello를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="0d584-133">hello 호출은 제외 하 고 흐름 로그를 활성화할 때와 동일한 hello **false** 사용 하도록 설정 하는 hello 속성에 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

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

<span data-ttu-id="0d584-134">hello에서 응답이 반환 되었습니다 hello 위의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-134">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="query-flow-logs"></a><span data-ttu-id="0d584-135">흐름 로그 쿼리</span><span class="sxs-lookup"><span data-stu-id="0d584-135">Query flow logs</span></span>

<span data-ttu-id="0d584-136">쿼리 hello 흐름의 상태는 REST 호출 다음 hello를 네트워크 보안 그룹에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

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

<span data-ttu-id="0d584-137">hello 다음은 반환 하는 hello 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-137">hello following is an example of hello response returned:</span></span>

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

## <a name="download-a-flow-log"></a><span data-ttu-id="0d584-138">흐름 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="0d584-138">Download a flow log</span></span>

<span data-ttu-id="0d584-139">흐름 로그의 hello 저장소 위치를 만들 때 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="0d584-140">이러한 흐름 저장 된 로그 tooa 저장소 계정이 여기에서 다운로드할 수 있는 Microsoft Azure 저장소 탐색기는 편리한 도구 tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="0d584-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="0d584-141">저장소 계정이 지정 되어 있으면 hello 수정할 수 있는 위치에서 저장소 계정은 tooa 패킷 캡처 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d584-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="0d584-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0d584-142">Next steps</span></span>

<span data-ttu-id="0d584-143">너무 방법에 대해 알아봅니다[PowerBI와 NSG 흐름 로그를 시각화 합니다.](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="0d584-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="0d584-144">너무 방법에 대해 알아봅니다[오픈 소스 도구와 함께 NSG 흐름 로그를 시각화 합니다.](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="0d584-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
