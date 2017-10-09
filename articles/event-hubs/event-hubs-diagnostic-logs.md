---
title: "이벤트 허브 진단 로그 aaaAzure | Microsoft Docs"
description: "자세한 방법을 tooset Azure에서 이벤트 허브에 대 한 진단 로그를 합니다."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="19c6d-103">Event Hubs 진단 로그</span><span class="sxs-lookup"><span data-stu-id="19c6d-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="19c6d-104">Azure Event Hubs에 대해 다음 두 가지 유형의 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="19c6d-105">**[활동 로그](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="19c6d-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="19c6d-106">이러한 로그에는 작업에 대해 수행된 작업 관련 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="19c6d-107">hello 로그는 항상 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="19c6d-108">**[진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="19c6d-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="19c6d-109">작업에서 발생하는 모든 상황을 보다 잘 이해할 수 있도록 진단 로그를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="19c6d-110">진단은 hello ְ  업데이트 및 hello 작업이 실행 되는 동안 발생 하는 활동을 포함 하 여 hello 작업 삭제 될 때까지 hello 시간부터 커버 활동을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="19c6d-111">진단 로그 설정</span><span class="sxs-lookup"><span data-stu-id="19c6d-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="19c6d-112">진단 로그는 기본적으로 해제되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="19c6d-113">tooenable 진단 로그:</span><span class="sxs-lookup"><span data-stu-id="19c6d-113">tooenable diagnostic logs:</span></span>

1.  <span data-ttu-id="19c6d-114">Hello에 [Azure 포털](https://portal.azure.com)아래 **모니터링 + 관리**, 클릭 **진단 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![블레이드 탐색 toodiagnostic 로그](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="19c6d-116">Toomonitor hello 리소스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-116">Click hello resource you want toomonitor.</span></span>

3.  <span data-ttu-id="19c6d-117">**진단 켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-117">Click **Turn on diagnostics**.</span></span>

    ![진단 로그 설정](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="19c6d-119">**상태**에서 **켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-119">For **Status**, click **On**.</span></span>

    ![진단 로그의 hello 상태 변경](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="19c6d-121">원하는; 집합 hello 보관 대상 예를 들어 저장소 계정, 이벤트 허브 또는 Azure 로그 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-121">Set hello archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="19c6d-122">Hello 새 진단 설정을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="19c6d-123">새 설정은 약 10분 후에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="19c6d-124">그 후 로그가 hello에 구성 된 hello 보관 대상에 나타납니다 **진단 로그** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="19c6d-125">진단을 구성 하는 방법에 대 한 자세한 내용은 참조 hello [Azure 진단 로그의 개요](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="19c6d-126">진단 로그 범주</span><span class="sxs-lookup"><span data-stu-id="19c6d-126">Diagnostic logs categories</span></span>
<span data-ttu-id="19c6d-127">Event Hubs는 다음 두 가지 범주에 대한 진단 로그를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="19c6d-128">**ArchiveLogs**: 로그 관련 tooEvent 허브 아카이브 구체적으로, 관련된 tooarchive 오류를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-128">**ArchiveLogs**: logs related tooEvent Hubs archives, specifically, logs related tooarchive errors.</span></span>
* <span data-ttu-id="19c6d-129">**OperationalLogs**: 특히 이벤트 허브 작업 하는 동안 프로세스에 대 한 내용은 작업 유형, 이벤트 허브 만들기를 사용 하는 리소스를 포함 하 여 hello 및 hello hello 작업의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, hello operation type, including event hub creation, resources used, and hello status of hello operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="19c6d-130">진단 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="19c6d-130">Diagnostic logs schema</span></span>
<span data-ttu-id="19c6d-131">모든 로그는 JSON(JavaScript Object Notation) 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="19c6d-132">각 항목에 hello 다음 섹션에에서 설명 된 hello 형식을 사용 하는 문자열 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-132">Each entry has string fields that use hello format described in hello following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="19c6d-133">보관 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="19c6d-133">Archive logs schema</span></span>

<span data-ttu-id="19c6d-134">다음 표에 hello에 나열 된 요소를 포함 하는 보관 로그 JSON 문자열:</span><span class="sxs-lookup"><span data-stu-id="19c6d-134">Archive log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="19c6d-135">이름</span><span class="sxs-lookup"><span data-stu-id="19c6d-135">Name</span></span> | <span data-ttu-id="19c6d-136">설명</span><span class="sxs-lookup"><span data-stu-id="19c6d-136">Description</span></span>
------- | -------
<span data-ttu-id="19c6d-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="19c6d-137">TaskName</span></span> | <span data-ttu-id="19c6d-138">Hello 작업에 실패 한 클라이언트의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-138">Description of hello task that failed.</span></span>
<span data-ttu-id="19c6d-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="19c6d-139">ActivityId</span></span> | <span data-ttu-id="19c6d-140">추적에 사용되는 내부 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="19c6d-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="19c6d-141">trackingId</span></span> | <span data-ttu-id="19c6d-142">추적에 사용되는 내부 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="19c6d-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="19c6d-143">resourceId</span></span> | <span data-ttu-id="19c6d-144">Azure Resource Manager 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="19c6d-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="19c6d-145">eventHub</span></span> | <span data-ttu-id="19c6d-146">이벤트 허브 전체 이름(네임스페이스 이름 포함)입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="19c6d-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="19c6d-147">partitionId</span></span> | <span data-ttu-id="19c6d-148">데이터가 기록되는 이벤트 허브 파티션입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="19c6d-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="19c6d-149">archiveStep</span></span> | <span data-ttu-id="19c6d-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="19c6d-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="19c6d-151">startTime</span><span class="sxs-lookup"><span data-stu-id="19c6d-151">startTime</span></span> | <span data-ttu-id="19c6d-152">실패 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-152">Failure start time.</span></span>
<span data-ttu-id="19c6d-153">failures</span><span class="sxs-lookup"><span data-stu-id="19c6d-153">failures</span></span> | <span data-ttu-id="19c6d-154">실패가 발생한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-154">Number of times failure occurred.</span></span>
<span data-ttu-id="19c6d-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="19c6d-155">durationInSeconds</span></span> | <span data-ttu-id="19c6d-156">실패 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-156">Duration of failure.</span></span>
<span data-ttu-id="19c6d-157">Message</span><span class="sxs-lookup"><span data-stu-id="19c6d-157">message</span></span> | <span data-ttu-id="19c6d-158">오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-158">Error message.</span></span>
<span data-ttu-id="19c6d-159">카테고리</span><span class="sxs-lookup"><span data-stu-id="19c6d-159">category</span></span> | <span data-ttu-id="19c6d-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="19c6d-160">ArchiveLogs</span></span>

<span data-ttu-id="19c6d-161">hello 다음 코드는 아카이브 로그 JSON 문자열의 예:</span><span class="sxs-lookup"><span data-stu-id="19c6d-161">hello following code is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="19c6d-162">작업 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="19c6d-162">Operational logs schema</span></span>

<span data-ttu-id="19c6d-163">다음 표에 hello에 나열 된 요소를 포함 하는 작업 로그 JSON 문자열:</span><span class="sxs-lookup"><span data-stu-id="19c6d-163">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="19c6d-164">이름</span><span class="sxs-lookup"><span data-stu-id="19c6d-164">Name</span></span> | <span data-ttu-id="19c6d-165">설명</span><span class="sxs-lookup"><span data-stu-id="19c6d-165">Description</span></span>
------- | -------
<span data-ttu-id="19c6d-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="19c6d-166">ActivityId</span></span> | <span data-ttu-id="19c6d-167">내부 ID tootrack 목적을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-167">Internal ID, used tootrack purpose.</span></span>
<span data-ttu-id="19c6d-168">EventName</span><span class="sxs-lookup"><span data-stu-id="19c6d-168">EventName</span></span> | <span data-ttu-id="19c6d-169">작업 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-169">Operation name.</span></span>  
<span data-ttu-id="19c6d-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="19c6d-170">resourceId</span></span> | <span data-ttu-id="19c6d-171">Azure Resource Manager 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="19c6d-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="19c6d-172">SubscriptionId</span></span> | <span data-ttu-id="19c6d-173">구독 ID가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-173">Subscription ID.</span></span>
<span data-ttu-id="19c6d-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="19c6d-174">EventTimeString</span></span> | <span data-ttu-id="19c6d-175">작업 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-175">Operation time.</span></span>
<span data-ttu-id="19c6d-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="19c6d-176">EventProperties</span></span> | <span data-ttu-id="19c6d-177">작업 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-177">Operation properties.</span></span>
<span data-ttu-id="19c6d-178">가동 상태</span><span class="sxs-lookup"><span data-stu-id="19c6d-178">Status</span></span> | <span data-ttu-id="19c6d-179">작업 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-179">Operation status.</span></span>
<span data-ttu-id="19c6d-180">Caller</span><span class="sxs-lookup"><span data-stu-id="19c6d-180">Caller</span></span> | <span data-ttu-id="19c6d-181">작업 호출자(Azure Portal 또는 관리 클라이언트)입니다.</span><span class="sxs-lookup"><span data-stu-id="19c6d-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="19c6d-182">카테고리</span><span class="sxs-lookup"><span data-stu-id="19c6d-182">category</span></span> | <span data-ttu-id="19c6d-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="19c6d-183">OperationalLogs</span></span>

<span data-ttu-id="19c6d-184">hello 다음 코드는 작업 로그 JSON 문자열의 예:</span><span class="sxs-lookup"><span data-stu-id="19c6d-184">hello following code is an example of an operational log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="19c6d-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="19c6d-185">Next steps</span></span>
* [<span data-ttu-id="19c6d-186">소개 tooEvent 허브</span><span class="sxs-lookup"><span data-stu-id="19c6d-186">Introduction tooEvent Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="19c6d-187">이벤트 허브 API 개요</span><span class="sxs-lookup"><span data-stu-id="19c6d-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="19c6d-188">이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="19c6d-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
