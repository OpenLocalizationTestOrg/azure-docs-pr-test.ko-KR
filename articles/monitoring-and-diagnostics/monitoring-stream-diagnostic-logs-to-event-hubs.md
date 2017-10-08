---
title: "이벤트 허브 Namespace aaaStream Azure 진단 로그 tooan | Microsoft Docs"
description: "Azure 진단 toostream tooan 이벤트 허브 네임 스페이스를 기록 하는 방법에 대해 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a><span data-ttu-id="98a1a-103">Azure 진단 로그 tooan 이벤트 허브 Namespace 스트림</span><span class="sxs-lookup"><span data-stu-id="98a1a-103">Stream Azure Diagnostic Logs tooan Event Hubs Namespace</span></span>
<span data-ttu-id="98a1a-104">**[Azure 진단 로그](monitoring-overview-of-diagnostic-logs.md)**  거의 실시간으로 tooany hello 포털에서에서 기본 제공 "tooEvent 허브 내보내기" 옵션 hello를 사용 하 여 응용 프로그램에 스트리밍할 수 또는 사용 하 여 hello Azure PowerShell을 통해 진단 설정에 서비스 버스 규칙 ID를 환영 Cmdlet 또는 Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time tooany application using hello built-in “Export tooEvent Hubs” option in hello Portal, or by enabling hello Service Bus Rule ID in a diagnostic setting via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="98a1a-105">진단 로그 및 Event Hubs에서 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="98a1a-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="98a1a-106">다음 몇 가지 방법으로 hello 진단 로그에 대 한 기능을 스트리밍을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-106">Here are just a few ways you might use hello streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="98a1a-107">**스트림에 기록 too3rd 파티 로깅 및 원격 분석 시스템** – 시간이 지남에 따라 이벤트 허브는 hello 메커니즘 toopipe toothird 파티 Siem에서 진단 로그에 될 스트리밍과 로그 분석 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-107">**Stream logs too3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your diagnostic logs in toothird-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="98a1a-108">**"실행 부하 과다 경로" 데이터 tooPowerBI 스트리밍하여 서비스 상태를 보려면** – 이벤트 허브를 사용 하 여, 스트림 분석 및 PowerBI, Azure 서비스에 toonear 실시간 insights에서 진단 데이터를 쉽게 변형할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-108">**View service health by streaming “hot path” data tooPowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in toonear real-time insights on your Azure services.</span></span> <span data-ttu-id="98a1a-109">[이 설명서 문서에서는 이벤트 허브를 tooset 스트림 분석을 사용 하 여 데이터를 처리 하 고 출력을 출력으로 PowerBI를 사용 하는 방법에 대 한 훌륭한 개괄적](../stream-analytics/stream-analytics-power-bi-dashboard.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-109">[This documentation article gives a great overview of how tooset up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="98a1a-110">다음은 진단 로그로 설정하는 방법에 대한 몇 가지 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="98a1a-111">진단 로그의 범주에 대 한 이벤트 허브는 hello 포털 hello 옵션을 확인 하거나 tooselect hello 이름의 네임 스페이스가 hello로 시작 되 면 hello 이벤트 허브를 원하는 PowerShell을 통해 설정할 때 자동으로 생성 됩니다 **insights**.</span><span class="sxs-lookup"><span data-stu-id="98a1a-111">An event hub for a category of diagnostic logs is created automatically when you check hello option in hello portal or enable it through PowerShell, so you want tooselect hello event hub in hello namespace with hello name that starts with **insights-**.</span></span>
  * <span data-ttu-id="98a1a-112">hello SQL 코드 다음은 샘플 스트림 분석 쿼리를 사용할 수 있는 tooparse hello 로그 데이터를 모두 tooa PowerBI 테이블에서:</span><span class="sxs-lookup"><span data-stu-id="98a1a-112">hello following SQL code is a sample Stream Analytics query that you can use tooparse all hello log data in tooa PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="98a1a-113">**빌드 사용자 지정 원격 분석 및 로깅 플랫폼** 는 진단 수집 건물 하나, 확장성이 높은 hello 게시-구독에 대해 생각 방금 이벤트 허브의 특성 tooflexibly 수 있습니다. 또는 사용자가 작성 한 원격 분석 플랫폼을 이미 있는 경우- 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="98a1a-114">[Dan Rosanova 가이드 toousing 이벤트 허브는 세계적인 규모 원격 분석 플랫폼 여기에 참조](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-114">[See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="98a1a-115">진단 로그의 스트리밍 사용</span><span class="sxs-lookup"><span data-stu-id="98a1a-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="98a1a-116">Hello 포털을 통해 프로그래밍 방식으로 진단 로그의 스트리밍 또는 hello를 사용 하 여 사용 하도록 설정할 수 [Azure 모니터 REST Api](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings)합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-116">You can enable streaming of diagnostic logs programmatically, via hello portal, or using hello [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="98a1a-117">진단 설정을 만드는 두 가지 경우 모두 지정 하는 이벤트 허브 네임 스페이스 및 hello 로그 범주 및 메트릭을 toosend toohello 네임 스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and hello log categories and metrics you want toosend in toohello namespace.</span></span> <span data-ttu-id="98a1a-118">이벤트 허브를 사용 하도록 설정 하면 로그 범주별 hello 네임 스페이스에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-118">An event hub is created in hello namespace for each log category you enable.</span></span> <span data-ttu-id="98a1a-119">진단 **로그 범주**는 리소스가 수집할 수 있는 로그 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="98a1a-120">계산 리소스(예: VM 또는 서비스 패브릭)에서 진단 로그를 사용 및 스트리밍하려면 [여러 단계 집합을 거쳐야 합니다](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="98a1a-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="98a1a-121">서비스 버스 hello 또는 이벤트 허브 네임 스페이스가 없는 toobe hello hello 설정을 구성 하는 hello 사용자에 게 적합 한 RBAC 액세스 tooboth 구독으로 로그를 내보내는 hello 리소스와 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-121">hello Service Bus or Event Hubs namespace does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="98a1a-122">Hello 포털을 사용 하 여 스트림 진단 로그</span><span class="sxs-lookup"><span data-stu-id="98a1a-122">Stream diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="98a1a-123">Hello 포털 tooAzure 모니터를 탐색 하 고 클릭 **진단 설정**</span><span class="sxs-lookup"><span data-stu-id="98a1a-123">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure Monitor의 모니터링 섹션](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="98a1a-125">필요에 따라 리소스 그룹 또는 리소스 유형으로 hello 목록을 필터링 하려는 진단 설정 tooset hello 리소스 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-125">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="98a1a-126">선택한 hello 리소스에 설정이 없는 있으면 증명된 toocreate 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-126">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="98a1a-127">“진단 켜기”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-127">Click "Turn on diagnostics."</span></span>

   ![진단 설정 추가 - 기존 설정 없음](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="98a1a-129">Hello 리소스에 대 한 기존 설정을 없을 경우이 리소스에서 이미 구성 되어 있는 설정 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-129">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="98a1a-130">“진단 설정 추가”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-130">Click "Add diagnostic setting."</span></span>

   ![진단 설정 추가 - 기존 설정](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="98a1a-132">사용자 설정 이름을 지정 하 고 hello 확인란에 대 한 **스트림 tooan 이벤트 허브**, 프로그램에서 이벤트 허브 네임 스페이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-132">Give your setting a name and check hello box for **Stream tooan event hub**, then select an Event Hubs namespace.</span></span>
   
   ![진단 설정 추가 - 기존 설정](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="98a1a-134">hello 네임 스페이스 선택 됩니다 여기서 hello 이벤트 허브 (처음으로 스트리밍 진단 로그 경우) 만들어지거나 너무 스트리밍 (많은 경우 이미 해당 로그 범주 toothis 네임 스페이스는 스트리밍 리소스), hello을 정의 하는 hello 정책 hello 스트리밍 메커니즘에 있는 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-134">hello namespace selected will be where hello event hub is created (if this is your first time streaming diagnostic logs) or streamed too(if there are already resources that are streaming that log category toothis namespace), and hello policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="98a1a-135">이벤트 허브 관리, 송신, 수신 대기 권한을 오늘 필요 tooan 스트리밍 합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-135">Today, streaming tooan event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="98a1a-136">작성 하거나 네임 스페이스에 대 한 hello 포털 hello 구성 탭에서 이벤트 허브 네임 스페이스 공유 액세스 정책을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-136">You can create or modify Event Hubs namespace shared access policies in hello portal under hello Configure tab for your namespace.</span></span> <span data-ttu-id="98a1a-137">tooupdate 이러한 진단 설정 중 하나를 hello 클라이언트 hello 이벤트 허브 권한 부여 규칙에 hello ListKey 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-137">tooupdate one of these diagnostic settings, hello client must have hello ListKey permission on hello Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="98a1a-138">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-138">Click **Save**.</span></span>

<span data-ttu-id="98a1a-139">몇 분 후 hello 새 설정이이 리소스에 대 한 설정의 목록에 나타나고 새 이벤트 데이터는 생성 되는 즉시 진단 로그 toothat 저장소 계정 스트리밍됩니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-139">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are streamed toothat storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="98a1a-140">PowerShell Cmdlet을 통해</span><span class="sxs-lookup"><span data-stu-id="98a1a-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="98a1a-141">hello를 통해 스트리밍 tooenable [Azure PowerShell Cmdlet](insights-powershell-samples.md), hello를 사용할 수 있습니다 `Set-AzureRmDiagnosticSetting` 이러한 매개 변수를 사용 하 여 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="98a1a-141">tooenable streaming via hello [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use hello `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="98a1a-142">hello 서비스 버스 규칙 ID는이 형식의 문자열로: `{Service Bus resource ID}/authorizationrules/{key name}`, 예를 들어 `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-142">hello Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="98a1a-143">Azure CLI를 통해</span><span class="sxs-lookup"><span data-stu-id="98a1a-143">Via Azure CLI</span></span>
<span data-ttu-id="98a1a-144">hello를 통해 스트리밍 tooenable [Azure CLI](insights-cli-samples.md), hello를 사용할 수 있습니다 `insights diagnostic set` 이와 같은 명령을:</span><span class="sxs-lookup"><span data-stu-id="98a1a-144">tooenable streaming via hello [Azure CLI](insights-cli-samples.md), you can use hello `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="98a1a-145">Hello PowerShell Cmdlet에 대 한 설명 된 대로 서비스 버스 규칙 ID에 대 한 동일한 형식 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-145">Use hello same format for Service Bus Rule ID as explained for hello PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="98a1a-146">이벤트 허브에서 로그 데이터를 hello를 사용 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="98a1a-146">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="98a1a-147">다음은 Event Hubs의 샘플 출력 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-147">Here is sample output data from Event Hubs:</span></span>

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| <span data-ttu-id="98a1a-148">요소 이름</span><span class="sxs-lookup"><span data-stu-id="98a1a-148">Element Name</span></span> | <span data-ttu-id="98a1a-149">설명</span><span class="sxs-lookup"><span data-stu-id="98a1a-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="98a1a-150">레코드</span><span class="sxs-lookup"><span data-stu-id="98a1a-150">records</span></span> |<span data-ttu-id="98a1a-151">이 페이로드에 있는 모든 로그 이벤트의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="98a1a-152">실시간</span><span class="sxs-lookup"><span data-stu-id="98a1a-152">time</span></span> |<span data-ttu-id="98a1a-153">Hello 이벤트가 발생 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-153">Time at which hello event occurred.</span></span> |
| <span data-ttu-id="98a1a-154">카테고리</span><span class="sxs-lookup"><span data-stu-id="98a1a-154">category</span></span> |<span data-ttu-id="98a1a-155">이 이벤트에 대한 로그 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-155">Log category for this event.</span></span> |
| <span data-ttu-id="98a1a-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="98a1a-156">resourceId</span></span> |<span data-ttu-id="98a1a-157">이 이벤트를 생성 하는 hello 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-157">Resource ID of hello resource that generated this event.</span></span> |
| <span data-ttu-id="98a1a-158">operationName</span><span class="sxs-lookup"><span data-stu-id="98a1a-158">operationName</span></span> |<span data-ttu-id="98a1a-159">Hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-159">Name of hello operation.</span></span> |
| <span data-ttu-id="98a1a-160">level</span><span class="sxs-lookup"><span data-stu-id="98a1a-160">level</span></span> |<span data-ttu-id="98a1a-161">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-161">Optional.</span></span> <span data-ttu-id="98a1a-162">Hello 로그 이벤트 수준을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-162">Indicates hello log event level.</span></span> |
| <span data-ttu-id="98a1a-163">properties</span><span class="sxs-lookup"><span data-stu-id="98a1a-163">properties</span></span> |<span data-ttu-id="98a1a-164">Hello 이벤트의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-164">Properties of hello event.</span></span> |

<span data-ttu-id="98a1a-165">TooEvent 허브 스트리밍을 지원 되는 모든 리소스 공급자의 목록을 볼 수 있습니다 [여기](monitoring-overview-of-diagnostic-logs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-165">You can view a list of all resource providers that support streaming tooEvent Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="98a1a-166">계산 리소스의 스트림 데이터</span><span class="sxs-lookup"><span data-stu-id="98a1a-166">Stream data from Compute resources</span></span>
<span data-ttu-id="98a1a-167">Windows Azure 진단 에이전트가 hello를 사용 하 여 계산 리소스에서 진단 로그를 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-167">You can also stream diagnostic logs from Compute resources using hello Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="98a1a-168">[이 문서를 참조](../event-hubs/event-hubs-streaming-azure-diags-data.md) 방법에 대 한 tooset 위쪽에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="98a1a-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how tooset that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98a1a-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98a1a-169">Next steps</span></span>
* [<span data-ttu-id="98a1a-170">Azure 진단 로그에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="98a1a-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="98a1a-171">이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="98a1a-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

