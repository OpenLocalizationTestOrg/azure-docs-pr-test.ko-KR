---
title: "Event Hubs 네임스페이스로 Azure 진단 로그 스트림 | Microsoft Docs"
description: "Event Hubs 네임스페이스로 Azure 진단 로그를 스트림하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 01ba8ddfcf90e1368ac147296fd180f99420d96f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="stream-azure-diagnostic-logs-to-an-event-hubs-namespace"></a><span data-ttu-id="d6b33-103">Event Hubs 네임스페이스로 Azure 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="d6b33-103">Stream Azure Diagnostic Logs to an Event Hubs Namespace</span></span>
<span data-ttu-id="d6b33-104">포털에서 기본 제공되는 “Event Hubs로 내보내기” 옵션을 사용하거나 Azure PowerShell Cmdlet 또는 Azure CLI를 통해 진단 설정에서 Service Bus 규칙 ID를 사용하도록 설정하여 **[Azure 진단 로그](monitoring-overview-of-diagnostic-logs.md)**를 거의 실시간으로 응용 프로그램에 스트림할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time to any application using the built-in “Export to Event Hubs” option in the Portal, or by enabling the Service Bus Rule ID in a diagnostic setting via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="d6b33-105">진단 로그 및 Event Hubs에서 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="d6b33-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="d6b33-106">진단 로그의 스트리밍 기능을 사용할 수 있는 몇 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-106">Here are just a few ways you might use the streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="d6b33-107">**타사 로깅 및 원격 분석 시스템으로 로그 스트림** – 시간이 지나면서 Event Hubs 스트리밍은 진단 로그를 타사 SIEM 및 로그 분석 솔루션으로 파이핑하기 위한 메커니즘이 되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-107">**Stream logs to 3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your diagnostic logs in to third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="d6b33-108">**“실행 부하 과다 경로” 데이터를 PowerBI로 스트리밍하여 서비스 상태 보기** – Event Hubs, Stream Analytics 및 PowerBI를 사용하여 Azure 서비스에서 진단 데이터를 거의 실시간 정보로 간편하게 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-108">**View service health by streaming “hot path” data to PowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in to near real-time insights on your Azure services.</span></span> <span data-ttu-id="d6b33-109">[이 설명서 문서는 Event Hubs를 설정하고 Stream Analytics로 데이터를 처리하며 출력으로 PowerBI를 사용하는 방법에 대한 훌륭한 개요를 제공합니다](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="d6b33-109">[This documentation article gives a great overview of how to set up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="d6b33-110">다음은 진단 로그로 설정하는 방법에 대한 몇 가지 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="d6b33-111">진단 로그의 범주에 대한 이벤트 허브는 포털에서 해당 옵션을 선택하거나 PowerShell을 통해 사용하도록 설정하면 자동으로 생성되므로 **insights-**로 시작하는 이름의 네임스페이스에서 이벤트 허브를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-111">An event hub for a category of diagnostic logs is created automatically when you check the option in the portal or enable it through PowerShell, so you want to select the event hub in the namespace with the name that starts with **insights-**.</span></span>
  * <span data-ttu-id="d6b33-112">다음 SQL 코드는 모든 로그 데이터를 PowerBI 테이블로 간단히 구문 분석하는 데 사용할 수 있는 샘플 Stream Analytics 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-112">The following SQL code is a sample Stream Analytics query that you can use to parse all the log data in to a PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want to track]
    INTO
    [OutputSourceName – the PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="d6b33-113">**사용자 지정 원격 분석 및 로깅 플랫폼 빌드** – 사용자 지정 빌드 원격 분석 플랫폼이 이미 있거나 플랫폼 빌드에 대해 생각하고 있는 경우 이벤트 허브의 확장성 높은 게시-구독 특성을 통해 진단 로그를 유연하게 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="d6b33-114">[글로벌 확장 원격 분석 플랫폼에 이벤트 허브 사용에 대해서는 여기 Dan Rosanova의 가이드를 참조하세요.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)</span><span class="sxs-lookup"><span data-stu-id="d6b33-114">[See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="d6b33-115">진단 로그의 스트리밍 사용</span><span class="sxs-lookup"><span data-stu-id="d6b33-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="d6b33-116">프로그래밍 방식으로 포털을 통하거나 [Azure Monitor REST API](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings)를 사용하여 진단 로그의 스트리밍을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-116">You can enable streaming of diagnostic logs programmatically, via the portal, or using the [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="d6b33-117">어느 쪽이든 Event Hubs 네임스페이스를 지정하는 로그 설정과 네임스페이스로 전송하려는 로그 범주 및 메트릭을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and the log categories and metrics you want to send in to the namespace.</span></span> <span data-ttu-id="d6b33-118">이벤트 허브는 활성화한 각 로그 범주에 대한 네임스페이스에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-118">An event hub is created in the namespace for each log category you enable.</span></span> <span data-ttu-id="d6b33-119">진단 **로그 범주**는 리소스가 수집할 수 있는 로그 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="d6b33-120">계산 리소스(예: VM 또는 서비스 패브릭)에서 진단 로그를 사용 및 스트리밍하려면 [여러 단계 집합을 거쳐야 합니다](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="d6b33-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="d6b33-121">설정을 구성하는 사용자가 두 구독에 대한 적절한 RBAC 액세스를 가진 경우 Service Bus 또는 Event Hubs 네임스페이스는 로그를 내보내는 리소스와 동일한 구독을 가지고 있지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-121">The Service Bus or Event Hubs namespace does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-the-portal"></a><span data-ttu-id="d6b33-122">포털을 사용하여 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="d6b33-122">Stream diagnostic logs using the portal</span></span>
1. <span data-ttu-id="d6b33-123">포털에서 Azure Monitor로 이동하고 **진단 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-123">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure Monitor의 모니터링 섹션](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="d6b33-125">필요에 따라 리소스 그룹 또는 리소스 종류를 기준으로 목록을 필터링합니다. 그런 다음 진단 설정을 지정하려는 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-125">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="d6b33-126">선택한 리소스에 설정이 없는 경우, 설정을 만들라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-126">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="d6b33-127">“진단 켜기”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-127">Click "Turn on diagnostics."</span></span>

   ![진단 설정 추가 - 기존 설정 없음](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="d6b33-129">리소스에 기존 설정이 있는 경우 이 리소스에 이미 구성된 설정의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-129">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="d6b33-130">“진단 설정 추가”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-130">Click "Add diagnostic setting."</span></span>

   ![진단 설정 추가 - 기존 설정](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="d6b33-132">이름을 지정하고 **이벤트 허브로의 스트림**의 확인란을 선택한 다음, Event Hubs 네임스페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-132">Give your setting a name and check the box for **Stream to an event hub**, then select an Event Hubs namespace.</span></span>
   
   ![진단 설정 추가 - 기존 설정](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="d6b33-134">선택한 네임스페이스는 이벤트 허브가 생성(진단 로그를 처음으로 스트리밍하는 경우)되거나 스트림(해당 로그 범주를 이 네임스페이스로 스트리밍하는 리소스가 이미 있는 경우)되는 위치이며 정책은 스트리밍 메커니즘이 포함하는 사용 권한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-134">The namespace selected will be where the event hub is created (if this is your first time streaming diagnostic logs) or streamed to (if there are already resources that are streaming that log category to this namespace), and the policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="d6b33-135">현재, 이벤트 허브로 스트리밍하려면 관리, 보내기 및 수신 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-135">Today, streaming to an event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="d6b33-136">포털에서 네임스페이스에 대한 구성 탭 아래에서 Event Hubs 네임스페이스 공유 액세스 정책을 만들거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-136">You can create or modify Event Hubs namespace shared access policies in the portal under the Configure tab for your namespace.</span></span> <span data-ttu-id="d6b33-137">이러한 진단 설정 중 하나를 업데이트하려면 클라이언트에 Event Hubs 권한 부여 규칙에 대한 ListKey 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-137">To update one of these diagnostic settings, the client must have the ListKey permission on the Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="d6b33-138">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-138">Click **Save**.</span></span>

<span data-ttu-id="d6b33-139">몇 분 후 새 설정이 이 리소스에 대한 설정 목록에 표시되고, 새 이벤트 데이터가 생성되는 즉시 진단 로그가 해당 저장소 계정에 스트림됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-139">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are streamed to that storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="d6b33-140">PowerShell Cmdlet을 통해</span><span class="sxs-lookup"><span data-stu-id="d6b33-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="d6b33-141">[Azure PowerShell Cmdlet](insights-powershell-samples.md)을 통해 스트리밍을 사용하도록 설정하려면 다음 매개 변수와 함께 `Set-AzureRmDiagnosticSetting` cmdlet을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-141">To enable streaming via the [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use the `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="d6b33-142">서비스 버스 규칙 ID는 `{Service Bus resource ID}/authorizationrules/{key name}` 형식의 문자열입니다. 예를 들면 `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-142">The Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="d6b33-143">Azure CLI를 통해</span><span class="sxs-lookup"><span data-stu-id="d6b33-143">Via Azure CLI</span></span>
<span data-ttu-id="d6b33-144">[Azure CLI](insights-cli-samples.md)를 통해 스트리밍을 사용하도록 설정하려면 다음과 같이 `insights diagnostic set` 명령을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-144">To enable streaming via the [Azure CLI](insights-cli-samples.md), you can use the `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="d6b33-145">PowerShell Cmdlet에 대해 설명한 것처럼 서비스 버스 규칙 ID와 동일한 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-145">Use the same format for Service Bus Rule ID as explained for the PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="d6b33-146">이벤트 허브에서 로그 데이터를 사용하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="d6b33-146">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="d6b33-147">다음은 Event Hubs의 샘플 출력 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-147">Here is sample output data from Event Hubs:</span></span>

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

| <span data-ttu-id="d6b33-148">요소 이름</span><span class="sxs-lookup"><span data-stu-id="d6b33-148">Element Name</span></span> | <span data-ttu-id="d6b33-149">설명</span><span class="sxs-lookup"><span data-stu-id="d6b33-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d6b33-150">레코드</span><span class="sxs-lookup"><span data-stu-id="d6b33-150">records</span></span> |<span data-ttu-id="d6b33-151">이 페이로드에 있는 모든 로그 이벤트의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="d6b33-152">실시간</span><span class="sxs-lookup"><span data-stu-id="d6b33-152">time</span></span> |<span data-ttu-id="d6b33-153">이벤트가 발생한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-153">Time at which the event occurred.</span></span> |
| <span data-ttu-id="d6b33-154">카테고리</span><span class="sxs-lookup"><span data-stu-id="d6b33-154">category</span></span> |<span data-ttu-id="d6b33-155">이 이벤트에 대한 로그 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-155">Log category for this event.</span></span> |
| <span data-ttu-id="d6b33-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="d6b33-156">resourceId</span></span> |<span data-ttu-id="d6b33-157">이 이벤트를 생성한 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-157">Resource ID of the resource that generated this event.</span></span> |
| <span data-ttu-id="d6b33-158">operationName</span><span class="sxs-lookup"><span data-stu-id="d6b33-158">operationName</span></span> |<span data-ttu-id="d6b33-159">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-159">Name of the operation.</span></span> |
| <span data-ttu-id="d6b33-160">level</span><span class="sxs-lookup"><span data-stu-id="d6b33-160">level</span></span> |<span data-ttu-id="d6b33-161">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-161">Optional.</span></span> <span data-ttu-id="d6b33-162">로그 이벤트 수준을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-162">Indicates the log event level.</span></span> |
| <span data-ttu-id="d6b33-163">properties</span><span class="sxs-lookup"><span data-stu-id="d6b33-163">properties</span></span> |<span data-ttu-id="d6b33-164">이벤트의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-164">Properties of the event.</span></span> |

<span data-ttu-id="d6b33-165">Event Hubs로의 스트리밍을 지원하는 모든 리소스 공급자의 목록을 [여기](monitoring-overview-of-diagnostic-logs.md)에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-165">You can view a list of all resource providers that support streaming to Event Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="d6b33-166">계산 리소스의 스트림 데이터</span><span class="sxs-lookup"><span data-stu-id="d6b33-166">Stream data from Compute resources</span></span>
<span data-ttu-id="d6b33-167">Windows Azure 진단 에이전트를 사용하여 Compute 리소스에서 진단 로그를 스트림할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6b33-167">You can also stream diagnostic logs from Compute resources using the Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="d6b33-168">설정하는 방법은 [이 문서를 참조](../event-hubs/event-hubs-streaming-azure-diags-data.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="d6b33-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how to set that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6b33-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6b33-169">Next steps</span></span>
* [<span data-ttu-id="d6b33-170">Azure 진단 로그에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="d6b33-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="d6b33-171">이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="d6b33-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

