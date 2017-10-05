---
title: "Azure Batch 풀 크기 조정 완료 이벤트 | Microsoft Docs"
description: "Batch 풀 크기 조정 완료 이벤트에 대한 참조입니다."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 7072293d98526812cb42ce9c2f8e33bfcafaa149
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-complete-event"></a><span data-ttu-id="57b64-103">풀 크기 조정 완료 이벤트</span><span class="sxs-lookup"><span data-stu-id="57b64-103">Pool resize complete event</span></span>

 <span data-ttu-id="57b64-104">이 이벤트는 풀 크기 조정이 완료되거나 실패하면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-104">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="57b64-105">다음 예에서는 크기가 늘어나고 성공적으로 완료된 풀에 대한 풀 크기 조정 완료 이벤트의 본문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-105">The following example shows the body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "The operation succeeded"
}
```

|<span data-ttu-id="57b64-106">요소</span><span class="sxs-lookup"><span data-stu-id="57b64-106">Element</span></span>|<span data-ttu-id="57b64-107">형식</span><span class="sxs-lookup"><span data-stu-id="57b64-107">Type</span></span>|<span data-ttu-id="57b64-108">참고 사항</span><span class="sxs-lookup"><span data-stu-id="57b64-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="57b64-109">id</span><span class="sxs-lookup"><span data-stu-id="57b64-109">id</span></span>|<span data-ttu-id="57b64-110">String</span><span class="sxs-lookup"><span data-stu-id="57b64-110">String</span></span>|<span data-ttu-id="57b64-111">풀의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-111">The id of the pool.</span></span>|
|<span data-ttu-id="57b64-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="57b64-112">nodeDeallocationOption</span></span>|<span data-ttu-id="57b64-113">String</span><span class="sxs-lookup"><span data-stu-id="57b64-113">String</span></span>|<span data-ttu-id="57b64-114">풀 크기가 감소하는 경우 풀에서 노드를 제거할 수 있는 시기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-114">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="57b64-115">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="57b64-116">**requeue** – 실행 중인 태스크를 종료하고 해당 태스크를 다시 대기열에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="57b64-117">작업이 활성화되면 태스크가 다시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-117">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="57b64-118">태스크가 종료되는 즉시 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="57b64-119">**terminate** – 실행 중인 태스크를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="57b64-120">태스크가 다시 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-120">The tasks will not run again.</span></span> <span data-ttu-id="57b64-121">태스크가 종료되는 즉시 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="57b64-122">**taskcompletion** – 현재 실행 중인 태스크가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-122">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="57b64-123">대기하는 동안 새 태스크를 예약하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="57b64-124">모든 태스크가 완료되면 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="57b64-125">**Retaineddata** -현재 실행 중인 태스크가 완료될 때까지 기다린 후 모든 태스크 데이터 보존 기간이 만료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-125">**Retaineddata** -  Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="57b64-126">대기하는 동안 새 태스크를 예약하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="57b64-127">모든 태스크 보존 기간이 만료되면 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="57b64-128">기본값은 requeue입니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-128">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="57b64-129">풀 크기가 증가하는 경우 값이 **invalid**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-129">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="57b64-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="57b64-130">currentDedicated</span></span>|<span data-ttu-id="57b64-131">Int32</span><span class="sxs-lookup"><span data-stu-id="57b64-131">Int32</span></span>|<span data-ttu-id="57b64-132">현재 풀에 할당된 계산 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-132">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="57b64-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="57b64-133">targetDedicated</span></span>|<span data-ttu-id="57b64-134">Int32</span><span class="sxs-lookup"><span data-stu-id="57b64-134">Int32</span></span>|<span data-ttu-id="57b64-135">풀에 대해 요청된 계산 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-135">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="57b64-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="57b64-136">enableAutoScale</span></span>|<span data-ttu-id="57b64-137">Bool</span><span class="sxs-lookup"><span data-stu-id="57b64-137">Bool</span></span>|<span data-ttu-id="57b64-138">풀 크기가 시간이 지남에 따라 자동으로 조정되는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-138">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="57b64-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="57b64-139">isAutoPool</span></span>|<span data-ttu-id="57b64-140">Bool</span><span class="sxs-lookup"><span data-stu-id="57b64-140">Bool</span></span>|<span data-ttu-id="57b64-141">풀이 작업의 자동 풀 메커니즘을 통해 만들어졌는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-141">Specifies whether the pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="57b64-142">startTime</span><span class="sxs-lookup"><span data-stu-id="57b64-142">startTime</span></span>|<span data-ttu-id="57b64-143">DateTime</span><span class="sxs-lookup"><span data-stu-id="57b64-143">DateTime</span></span>|<span data-ttu-id="57b64-144">풀 크기 조정이 시작된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-144">The time the pool resize started.</span></span>|
|<span data-ttu-id="57b64-145">endTime</span><span class="sxs-lookup"><span data-stu-id="57b64-145">endTime</span></span>|<span data-ttu-id="57b64-146">DateTime</span><span class="sxs-lookup"><span data-stu-id="57b64-146">DateTime</span></span>|<span data-ttu-id="57b64-147">풀 크기 조정이 완료된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-147">The time the pool resize completed.</span></span>|
|<span data-ttu-id="57b64-148">resultCode</span><span class="sxs-lookup"><span data-stu-id="57b64-148">resultCode</span></span>|<span data-ttu-id="57b64-149">string</span><span class="sxs-lookup"><span data-stu-id="57b64-149">String</span></span>|<span data-ttu-id="57b64-150">크기 조정의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-150">The result of the resize.</span></span>|
|<span data-ttu-id="57b64-151">resultMessage</span><span class="sxs-lookup"><span data-stu-id="57b64-151">resultMessage</span></span>|<span data-ttu-id="57b64-152">string</span><span class="sxs-lookup"><span data-stu-id="57b64-152">String</span></span>|<span data-ttu-id="57b64-153">크기 조정 오류에 결과의 세부 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-153">The resize error includes the details of the result.</span></span><br /><br /> <span data-ttu-id="57b64-154">크기 조정이 성공적으로 완료되면 작업에 성공했다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="57b64-154">If the resize completed successfully it states that the operation succeeded.</span></span>|