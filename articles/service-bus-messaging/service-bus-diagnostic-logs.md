---
title: "Azure Service Bus 진단 로그 | Microsoft Docs"
description: "Azure에서 Service Bus에 대한 진단 로그를 설정하는 방법을 알아봅니다."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: 72e18444c83b84c5191a0aab3dc6983517167dd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="03ef2-103">Service Bus 진단 로그</span><span class="sxs-lookup"><span data-stu-id="03ef2-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="03ef2-104">Azure Service Bus에 대해 다음 두 가지 유형의 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="03ef2-105">**[활동 로그](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="03ef2-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="03ef2-106">이러한 로그에는 작업에 대해 수행된 작업 관련 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="03ef2-107">로그는 항상 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-107">The logs are always enabled.</span></span>
* <span data-ttu-id="03ef2-108">**[진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="03ef2-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="03ef2-109">작업에서 발생하는 모든 상황을 보다 잘 이해할 수 있도록 진단 로그를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="03ef2-110">진단 로그는 업데이트 및 작업이 실행 중일 때 발생하는 활동을 비롯하여 작업이 만들어질 때부터 삭제될 때까지의 모든 활동을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="03ef2-111">진단 로그 설정</span><span class="sxs-lookup"><span data-stu-id="03ef2-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="03ef2-112">진단 로그는 기본적으로 해제되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="03ef2-113">진단 로그를 활성화하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-113">To enable diagnostic logs, perform the following steps:</span></span>

1.  <span data-ttu-id="03ef2-114">[Azure Portal](https://portal.azure.com)의 **모니터링 + 관리**에서 **진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![진단 로그에 대한 블레이드 탐색](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="03ef2-116">모니터링하려는 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-116">Click the resource you want to monitor.</span></span>  

3.  <span data-ttu-id="03ef2-117">**진단 켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-117">Click **Turn on diagnostics**.</span></span>

    ![진단 로그 사용](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="03ef2-119">**상태**에서 **켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-119">For **Status**, click **On**.</span></span>

    ![진단 로그 상태 변경](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="03ef2-121">저장소 계정, 이벤트 허브 또는 Azure Log Analytics와 같이 원하는 보관 대상을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-121">Set the archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="03ef2-122">새 진단 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="03ef2-123">새 설정은 약 10분 후에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="03ef2-124">그런 다음 구성된 보관 대상의 **진단 로그** 블레이드에 로그가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="03ef2-125">진단 구성에 대한 자세한 내용은 [Azure 진단 로그 개요](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03ef2-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="03ef2-126">진단 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="03ef2-126">Diagnostic logs schema</span></span>

<span data-ttu-id="03ef2-127">모든 로그는 JSON(JavaScript Object Notation) 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="03ef2-128">각 항목에는 다음 섹션에 설명된 형식을 사용하는 문자열 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-128">Each entry has string fields that use the format described in the following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="03ef2-129">작업 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="03ef2-129">Operational logs schema</span></span>

<span data-ttu-id="03ef2-130">**OperationalLogs** 범주의 로그는 Service Bus 작업 중 발생하는 일을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-130">Logs in the **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="03ef2-131">특히 이러한 로그는 큐 만들기, 사용된 리소스 및 작업 상태를 비롯한 작업 형식을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-131">Specifically, these logs capture the operation type, including queue creation, resources used, and the status of the operation.</span></span>

<span data-ttu-id="03ef2-132">작업 로그 JSON 문자열에는 다음 표에 나열된 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-132">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="03ef2-133">이름</span><span class="sxs-lookup"><span data-stu-id="03ef2-133">Name</span></span> | <span data-ttu-id="03ef2-134">설명</span><span class="sxs-lookup"><span data-stu-id="03ef2-134">Description</span></span>
------- | -------
<span data-ttu-id="03ef2-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="03ef2-135">ActivityId</span></span> | <span data-ttu-id="03ef2-136">추적에 사용되는 내부 ID</span><span class="sxs-lookup"><span data-stu-id="03ef2-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="03ef2-137">EventName</span><span class="sxs-lookup"><span data-stu-id="03ef2-137">EventName</span></span> | <span data-ttu-id="03ef2-138">작업 이름</span><span class="sxs-lookup"><span data-stu-id="03ef2-138">Operation name</span></span>           
<span data-ttu-id="03ef2-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="03ef2-139">resourceId</span></span> | <span data-ttu-id="03ef2-140">Azure Resource Manager 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="03ef2-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="03ef2-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="03ef2-141">SubscriptionId</span></span> | <span data-ttu-id="03ef2-142">구독 ID</span><span class="sxs-lookup"><span data-stu-id="03ef2-142">Subscription ID</span></span>
<span data-ttu-id="03ef2-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="03ef2-143">EventTimeString</span></span> | <span data-ttu-id="03ef2-144">작업 시간</span><span class="sxs-lookup"><span data-stu-id="03ef2-144">Operation time</span></span>
<span data-ttu-id="03ef2-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="03ef2-145">EventProperties</span></span> | <span data-ttu-id="03ef2-146">작업 속성</span><span class="sxs-lookup"><span data-stu-id="03ef2-146">Operation properties</span></span>
<span data-ttu-id="03ef2-147">가동 상태</span><span class="sxs-lookup"><span data-stu-id="03ef2-147">Status</span></span> | <span data-ttu-id="03ef2-148">작업 상태</span><span class="sxs-lookup"><span data-stu-id="03ef2-148">Operation status</span></span>
<span data-ttu-id="03ef2-149">Caller</span><span class="sxs-lookup"><span data-stu-id="03ef2-149">Caller</span></span> | <span data-ttu-id="03ef2-150">작업 호출자(Azure Portal 또는 관리 클라이언트)</span><span class="sxs-lookup"><span data-stu-id="03ef2-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="03ef2-151">카테고리</span><span class="sxs-lookup"><span data-stu-id="03ef2-151">category</span></span> | <span data-ttu-id="03ef2-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="03ef2-152">OperationalLogs</span></span>

<span data-ttu-id="03ef2-153">작업 로그 JSON 문자열 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="03ef2-153">Here's an example of an operational log JSON string:</span></span>

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="03ef2-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03ef2-154">Next steps</span></span>

<span data-ttu-id="03ef2-155">Service Bus에 대한 자세한 내용을 보려면 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="03ef2-155">Visit the following links to learn more about Service Bus:</span></span>

* [<span data-ttu-id="03ef2-156">Service Bus 소개</span><span class="sxs-lookup"><span data-stu-id="03ef2-156">Introduction to Service Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="03ef2-157">Service Bus 시작</span><span class="sxs-lookup"><span data-stu-id="03ef2-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
