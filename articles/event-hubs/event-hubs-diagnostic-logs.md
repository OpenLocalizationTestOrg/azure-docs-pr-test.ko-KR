---
title: "Azure Event Hubs 진단 로그 | Microsoft Docs"
description: "Azure에서 이벤트 허브의 진단 로그를 설정하는 방법을 배웁니다."
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
ms.openlocfilehash: 09bc62f4918635419d74ef3ae400a41d4ce58b5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="49edd-103">Event Hubs 진단 로그</span><span class="sxs-lookup"><span data-stu-id="49edd-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="49edd-104">Azure Event Hubs에 대해 다음 두 가지 유형의 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="49edd-105">**[활동 로그](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="49edd-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="49edd-106">이러한 로그에는 작업에 대해 수행된 작업 관련 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="49edd-107">로그는 항상 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-107">The logs are always enabled.</span></span>
* <span data-ttu-id="49edd-108">**[진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="49edd-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="49edd-109">작업에서 발생하는 모든 상황을 보다 잘 이해할 수 있도록 진단 로그를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="49edd-110">진단 로그는 업데이트 및 작업이 실행 중일 때 발생하는 활동을 비롯하여 작업이 만들어질 때부터 삭제될 때까지의 모든 활동을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="49edd-111">진단 로그 설정</span><span class="sxs-lookup"><span data-stu-id="49edd-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="49edd-112">진단 로그는 기본적으로 해제되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="49edd-113">진단 로그를 사용하도록 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="49edd-113">To enable diagnostic logs:</span></span>

1.  <span data-ttu-id="49edd-114">[Azure Portal](https://portal.azure.com)의 **모니터링 + 관리**에서 **진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![진단 로그에 대한 블레이드 탐색](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="49edd-116">모니터링하려는 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-116">Click the resource you want to monitor.</span></span>

3.  <span data-ttu-id="49edd-117">**진단 켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-117">Click **Turn on diagnostics**.</span></span>

    ![진단 로그 설정](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="49edd-119">**상태**에서 **켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-119">For **Status**, click **On**.</span></span>

    ![진단 로그의 상태 변경](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="49edd-121">저장소 계정, 이벤트 허브 또는 Azure Log Analytics와 같이 원하는 보관 대상을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-121">Set the archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="49edd-122">새 진단 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="49edd-123">새 설정은 약 10분 후에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="49edd-124">그런 다음 구성된 보관 대상의 **진단 로그** 블레이드에 로그가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="49edd-125">진단 구성에 대한 자세한 내용은 [Azure 진단 로그 개요](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49edd-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="49edd-126">진단 로그 범주</span><span class="sxs-lookup"><span data-stu-id="49edd-126">Diagnostic logs categories</span></span>
<span data-ttu-id="49edd-127">Event Hubs는 다음 두 가지 범주에 대한 진단 로그를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="49edd-128">**ArchiveLogs:** 이벤트 허브 보관, 특히 보관 오류와 관련된 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-128">**ArchiveLogs**: logs related to Event Hubs archives, specifically, logs related to archive errors.</span></span>
* <span data-ttu-id="49edd-129">**OperationalLogs:** Event Hubs 작업 중 발생하는 사항, 특히 이벤트 허브 생성, 사용된 리소스, 작업 상태와 같은 작업 유형에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, the operation type, including event hub creation, resources used, and the status of the operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="49edd-130">진단 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="49edd-130">Diagnostic logs schema</span></span>
<span data-ttu-id="49edd-131">모든 로그는 JSON(JavaScript Object Notation) 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="49edd-132">각 항목에는 다음 섹션에 설명된 형식을 사용하는 문자열 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-132">Each entry has string fields that use the format described in the following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="49edd-133">보관 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="49edd-133">Archive logs schema</span></span>

<span data-ttu-id="49edd-134">보관 로그 JSON 문자열에는 다음 표에 나열된 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-134">Archive log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="49edd-135">이름</span><span class="sxs-lookup"><span data-stu-id="49edd-135">Name</span></span> | <span data-ttu-id="49edd-136">설명</span><span class="sxs-lookup"><span data-stu-id="49edd-136">Description</span></span>
------- | -------
<span data-ttu-id="49edd-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="49edd-137">TaskName</span></span> | <span data-ttu-id="49edd-138">실패한 작업에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-138">Description of the task that failed.</span></span>
<span data-ttu-id="49edd-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="49edd-139">ActivityId</span></span> | <span data-ttu-id="49edd-140">추적에 사용되는 내부 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="49edd-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="49edd-141">trackingId</span></span> | <span data-ttu-id="49edd-142">추적에 사용되는 내부 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="49edd-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="49edd-143">resourceId</span></span> | <span data-ttu-id="49edd-144">Azure Resource Manager 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="49edd-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="49edd-145">eventHub</span></span> | <span data-ttu-id="49edd-146">이벤트 허브 전체 이름(네임스페이스 이름 포함)입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="49edd-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="49edd-147">partitionId</span></span> | <span data-ttu-id="49edd-148">데이터가 기록되는 이벤트 허브 파티션입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="49edd-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="49edd-149">archiveStep</span></span> | <span data-ttu-id="49edd-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="49edd-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="49edd-151">startTime</span><span class="sxs-lookup"><span data-stu-id="49edd-151">startTime</span></span> | <span data-ttu-id="49edd-152">실패 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-152">Failure start time.</span></span>
<span data-ttu-id="49edd-153">failures</span><span class="sxs-lookup"><span data-stu-id="49edd-153">failures</span></span> | <span data-ttu-id="49edd-154">실패가 발생한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-154">Number of times failure occurred.</span></span>
<span data-ttu-id="49edd-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="49edd-155">durationInSeconds</span></span> | <span data-ttu-id="49edd-156">실패 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-156">Duration of failure.</span></span>
<span data-ttu-id="49edd-157">Message</span><span class="sxs-lookup"><span data-stu-id="49edd-157">message</span></span> | <span data-ttu-id="49edd-158">오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-158">Error message.</span></span>
<span data-ttu-id="49edd-159">카테고리</span><span class="sxs-lookup"><span data-stu-id="49edd-159">category</span></span> | <span data-ttu-id="49edd-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="49edd-160">ArchiveLogs</span></span>

<span data-ttu-id="49edd-161">다음 코드는 보관 로그 JSON 문자열에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-161">The following code is an example of an archive log JSON string:</span></span>

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
     "message": "Microsoft.WindowsAzure.Storage.StorageException: The remote server returned an error: (404) Not Found. ---> System.Net.WebException: The remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="49edd-162">작업 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="49edd-162">Operational logs schema</span></span>

<span data-ttu-id="49edd-163">작업 로그 JSON 문자열에는 다음 표에 나열된 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-163">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="49edd-164">이름</span><span class="sxs-lookup"><span data-stu-id="49edd-164">Name</span></span> | <span data-ttu-id="49edd-165">설명</span><span class="sxs-lookup"><span data-stu-id="49edd-165">Description</span></span>
------- | -------
<span data-ttu-id="49edd-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="49edd-166">ActivityId</span></span> | <span data-ttu-id="49edd-167">추적 목적에 사용되는 내부 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-167">Internal ID, used to track purpose.</span></span>
<span data-ttu-id="49edd-168">EventName</span><span class="sxs-lookup"><span data-stu-id="49edd-168">EventName</span></span> | <span data-ttu-id="49edd-169">작업 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-169">Operation name.</span></span>  
<span data-ttu-id="49edd-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="49edd-170">resourceId</span></span> | <span data-ttu-id="49edd-171">Azure Resource Manager 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="49edd-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="49edd-172">SubscriptionId</span></span> | <span data-ttu-id="49edd-173">구독 ID가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-173">Subscription ID.</span></span>
<span data-ttu-id="49edd-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="49edd-174">EventTimeString</span></span> | <span data-ttu-id="49edd-175">작업 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-175">Operation time.</span></span>
<span data-ttu-id="49edd-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="49edd-176">EventProperties</span></span> | <span data-ttu-id="49edd-177">작업 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-177">Operation properties.</span></span>
<span data-ttu-id="49edd-178">가동 상태</span><span class="sxs-lookup"><span data-stu-id="49edd-178">Status</span></span> | <span data-ttu-id="49edd-179">작업 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-179">Operation status.</span></span>
<span data-ttu-id="49edd-180">Caller</span><span class="sxs-lookup"><span data-stu-id="49edd-180">Caller</span></span> | <span data-ttu-id="49edd-181">작업 호출자(Azure Portal 또는 관리 클라이언트)입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="49edd-182">카테고리</span><span class="sxs-lookup"><span data-stu-id="49edd-182">category</span></span> | <span data-ttu-id="49edd-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="49edd-183">OperationalLogs</span></span>

<span data-ttu-id="49edd-184">다음 코드는 작업 로그 JSON 문자열에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="49edd-184">The following code is an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="49edd-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49edd-185">Next steps</span></span>
* [<span data-ttu-id="49edd-186">Event Hubs 소개</span><span class="sxs-lookup"><span data-stu-id="49edd-186">Introduction to Event Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="49edd-187">이벤트 허브 API 개요</span><span class="sxs-lookup"><span data-stu-id="49edd-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="49edd-188">이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="49edd-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
