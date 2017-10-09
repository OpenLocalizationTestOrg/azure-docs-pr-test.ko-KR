---
title: "서비스 버스 진단 로그 aaaAzure | Microsoft Docs"
description: "자세한 방법을 tooset Azure에서 서비스 버스에 대 한 진단 로그를 합니다."
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
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="fed30-103">Service Bus 진단 로그</span><span class="sxs-lookup"><span data-stu-id="fed30-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="fed30-104">Azure Service Bus에 대해 다음 두 가지 유형의 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="fed30-105">**[활동 로그](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="fed30-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="fed30-106">이러한 로그에는 작업에 대해 수행된 작업 관련 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="fed30-107">hello 로그는 항상 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="fed30-108">**[진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="fed30-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="fed30-109">작업에서 발생하는 모든 상황을 보다 잘 이해할 수 있도록 진단 로그를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="fed30-110">진단은 hello ְ  업데이트 및 hello 작업이 실행 되는 동안 발생 하는 활동을 포함 하 여 hello 작업 삭제 될 때까지 hello 시간부터 커버 활동을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="fed30-111">진단 로그 설정</span><span class="sxs-lookup"><span data-stu-id="fed30-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="fed30-112">진단 로그는 기본적으로 해제되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="fed30-113">tooenable 진단 로그 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-113">tooenable diagnostic logs, perform hello following steps:</span></span>

1.  <span data-ttu-id="fed30-114">Hello에 [Azure 포털](https://portal.azure.com)아래 **모니터링 + 관리**, 클릭 **진단 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![블레이드 탐색 toodiagnostic 로그](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="fed30-116">Toomonitor hello 리소스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-116">Click hello resource you want toomonitor.</span></span>  

3.  <span data-ttu-id="fed30-117">**진단 켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-117">Click **Turn on diagnostics**.</span></span>

    ![진단 로그 사용](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="fed30-119">**상태**에서 **켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-119">For **Status**, click **On**.</span></span>

    ![진단 로그 상태 변경](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="fed30-121">원하는; 집합 hello 보관 대상 예를 들어 저장소 계정, 이벤트 허브 또는 Azure 로그 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-121">Set hello archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="fed30-122">Hello 새 진단 설정을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="fed30-123">새 설정은 약 10분 후에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="fed30-124">그 후 로그가 hello에 구성 된 hello 보관 대상에 나타납니다 **진단 로그** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="fed30-125">진단을 구성 하는 방법에 대 한 자세한 내용은 참조 hello [Azure 진단 로그의 개요](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="fed30-126">진단 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="fed30-126">Diagnostic logs schema</span></span>

<span data-ttu-id="fed30-127">모든 로그는 JSON(JavaScript Object Notation) 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="fed30-128">각 항목에 hello 다음 섹션에에서 설명 된 hello 형식을 사용 하는 문자열 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-128">Each entry has string fields that use hello format described in hello following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="fed30-129">작업 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="fed30-129">Operational logs schema</span></span>

<span data-ttu-id="fed30-130">Hello 로그인 **OperationalLogs** 범주 서비스 버스 작업 중 진행 상황을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-130">Logs in hello **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="fed30-131">특히, 이러한 로그를 만드는 큐를 사용 하는 리소스를 포함 하 여 hello 작업 유형을 캡처하고 hello 작업의 상태를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-131">Specifically, these logs capture hello operation type, including queue creation, resources used, and hello status of hello operation.</span></span>

<span data-ttu-id="fed30-132">다음 표에 hello에 나열 된 요소를 포함 하는 작업 로그 JSON 문자열:</span><span class="sxs-lookup"><span data-stu-id="fed30-132">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="fed30-133">이름</span><span class="sxs-lookup"><span data-stu-id="fed30-133">Name</span></span> | <span data-ttu-id="fed30-134">설명</span><span class="sxs-lookup"><span data-stu-id="fed30-134">Description</span></span>
------- | -------
<span data-ttu-id="fed30-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="fed30-135">ActivityId</span></span> | <span data-ttu-id="fed30-136">추적에 사용되는 내부 ID</span><span class="sxs-lookup"><span data-stu-id="fed30-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="fed30-137">EventName</span><span class="sxs-lookup"><span data-stu-id="fed30-137">EventName</span></span> | <span data-ttu-id="fed30-138">작업 이름</span><span class="sxs-lookup"><span data-stu-id="fed30-138">Operation name</span></span>           
<span data-ttu-id="fed30-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="fed30-139">resourceId</span></span> | <span data-ttu-id="fed30-140">Azure Resource Manager 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="fed30-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="fed30-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="fed30-141">SubscriptionId</span></span> | <span data-ttu-id="fed30-142">구독 ID</span><span class="sxs-lookup"><span data-stu-id="fed30-142">Subscription ID</span></span>
<span data-ttu-id="fed30-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="fed30-143">EventTimeString</span></span> | <span data-ttu-id="fed30-144">작업 시간</span><span class="sxs-lookup"><span data-stu-id="fed30-144">Operation time</span></span>
<span data-ttu-id="fed30-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="fed30-145">EventProperties</span></span> | <span data-ttu-id="fed30-146">작업 속성</span><span class="sxs-lookup"><span data-stu-id="fed30-146">Operation properties</span></span>
<span data-ttu-id="fed30-147">가동 상태</span><span class="sxs-lookup"><span data-stu-id="fed30-147">Status</span></span> | <span data-ttu-id="fed30-148">작업 상태</span><span class="sxs-lookup"><span data-stu-id="fed30-148">Operation status</span></span>
<span data-ttu-id="fed30-149">Caller</span><span class="sxs-lookup"><span data-stu-id="fed30-149">Caller</span></span> | <span data-ttu-id="fed30-150">작업 호출자(Azure Portal 또는 관리 클라이언트)</span><span class="sxs-lookup"><span data-stu-id="fed30-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="fed30-151">카테고리</span><span class="sxs-lookup"><span data-stu-id="fed30-151">category</span></span> | <span data-ttu-id="fed30-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="fed30-152">OperationalLogs</span></span>

<span data-ttu-id="fed30-153">작업 로그 JSON 문자열 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fed30-153">Here's an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fed30-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fed30-154">Next steps</span></span>

<span data-ttu-id="fed30-155">서비스 버스에 대 한 자세한 링크 toolearn 다음 hello 방문.</span><span class="sxs-lookup"><span data-stu-id="fed30-155">Visit hello following links toolearn more about Service Bus:</span></span>

* [<span data-ttu-id="fed30-156">소개 tooService 버스</span><span class="sxs-lookup"><span data-stu-id="fed30-156">Introduction tooService Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="fed30-157">Service Bus 시작</span><span class="sxs-lookup"><span data-stu-id="fed30-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
