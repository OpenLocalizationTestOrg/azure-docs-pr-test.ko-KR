---
title: "aaa \"Azure 배치 풀 완료 이벤트를 크기 조정 | \"Microsoft Docs"
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
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a><span data-ttu-id="b2c2d-103">풀 크기 조정 완료 이벤트</span><span class="sxs-lookup"><span data-stu-id="b2c2d-103">Pool resize complete event</span></span>

 <span data-ttu-id="b2c2d-104">이 이벤트는 풀 크기 조정이 완료되거나 실패하면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-104">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="b2c2d-105">hello 다음 예제에서는 크기가 증가 하 고 성공적으로 완료 하는 풀에 대 한 풀 크기 조정 전체 이벤트의 hello 본문</span><span class="sxs-lookup"><span data-stu-id="b2c2d-105">hello following example shows hello body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

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
    "resizeError": "hello operation succeeded"
}
```

|<span data-ttu-id="b2c2d-106">요소</span><span class="sxs-lookup"><span data-stu-id="b2c2d-106">Element</span></span>|<span data-ttu-id="b2c2d-107">형식</span><span class="sxs-lookup"><span data-stu-id="b2c2d-107">Type</span></span>|<span data-ttu-id="b2c2d-108">참고 사항</span><span class="sxs-lookup"><span data-stu-id="b2c2d-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="b2c2d-109">id</span><span class="sxs-lookup"><span data-stu-id="b2c2d-109">id</span></span>|<span data-ttu-id="b2c2d-110">문자열</span><span class="sxs-lookup"><span data-stu-id="b2c2d-110">String</span></span>|<span data-ttu-id="b2c2d-111">hello 풀의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="b2c2d-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="b2c2d-112">nodeDeallocationOption</span></span>|<span data-ttu-id="b2c2d-113">문자열</span><span class="sxs-lookup"><span data-stu-id="b2c2d-113">String</span></span>|<span data-ttu-id="b2c2d-114">Hello 풀 크기가 감소 하는 경우 노드 hello 풀에서 제거할 수 있는 시기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-114">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="b2c2d-115">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="b2c2d-116">**requeue** – 실행 중인 태스크를 종료하고 해당 태스크를 다시 대기열에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="b2c2d-117">hello 작업이 사용 되는지 hello 작업 다시 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-117">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="b2c2d-118">태스크가 종료되는 즉시 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="b2c2d-119">**terminate** – 실행 중인 태스크를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="b2c2d-120">hello 작업 다시 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-120">hello tasks will not run again.</span></span> <span data-ttu-id="b2c2d-121">태스크가 종료되는 즉시 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="b2c2d-122">**taskcompletion** – 현재 작업 toocomplete 실행 되 고 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-122">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="b2c2d-123">대기하는 동안 새 태스크를 예약하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="b2c2d-124">모든 태스크가 완료되면 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="b2c2d-125">**Retaineddata** -현재 실행 되는 작업 toocomplete을 모든 작업 데이터 보존 기간 tooexpire 기다리세요.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-125">**Retaineddata** -  Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="b2c2d-126">대기하는 동안 새 태스크를 예약하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="b2c2d-127">모든 태스크 보존 기간이 만료되면 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="b2c2d-128">hello 기본값은 큐에 다시 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-128">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="b2c2d-129">Hello 풀 크기가 계속 증가 하는 경우 hello 값이 너무 설정**잘못 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-129">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="b2c2d-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="b2c2d-130">currentDedicated</span></span>|<span data-ttu-id="b2c2d-131">Int32</span><span class="sxs-lookup"><span data-stu-id="b2c2d-131">Int32</span></span>|<span data-ttu-id="b2c2d-132">hello 계산 노드 수는 현재 toohello 풀을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-132">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="b2c2d-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="b2c2d-133">targetDedicated</span></span>|<span data-ttu-id="b2c2d-134">Int32</span><span class="sxs-lookup"><span data-stu-id="b2c2d-134">Int32</span></span>|<span data-ttu-id="b2c2d-135">hello hello 풀에 대해 요청 된 계산 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-135">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="b2c2d-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="b2c2d-136">enableAutoScale</span></span>|<span data-ttu-id="b2c2d-137">Bool</span><span class="sxs-lookup"><span data-stu-id="b2c2d-137">Bool</span></span>|<span data-ttu-id="b2c2d-138">Hello 풀 크기 시간에 따라 자동으로 조정 되는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-138">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="b2c2d-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="b2c2d-139">isAutoPool</span></span>|<span data-ttu-id="b2c2d-140">Bool</span><span class="sxs-lookup"><span data-stu-id="b2c2d-140">Bool</span></span>|<span data-ttu-id="b2c2d-141">작업의 자동 풀 메커니즘을 통해 hello 풀 생성 되는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-141">Specifies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="b2c2d-142">startTime</span><span class="sxs-lookup"><span data-stu-id="b2c2d-142">startTime</span></span>|<span data-ttu-id="b2c2d-143">DateTime</span><span class="sxs-lookup"><span data-stu-id="b2c2d-143">DateTime</span></span>|<span data-ttu-id="b2c2d-144">시작 hello 풀 크기 조정 하는 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-144">hello time hello pool resize started.</span></span>|
|<span data-ttu-id="b2c2d-145">endTime</span><span class="sxs-lookup"><span data-stu-id="b2c2d-145">endTime</span></span>|<span data-ttu-id="b2c2d-146">DateTime</span><span class="sxs-lookup"><span data-stu-id="b2c2d-146">DateTime</span></span>|<span data-ttu-id="b2c2d-147">hello hello 풀 크기 조정 완료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-147">hello time hello pool resize completed.</span></span>|
|<span data-ttu-id="b2c2d-148">resultCode</span><span class="sxs-lookup"><span data-stu-id="b2c2d-148">resultCode</span></span>|<span data-ttu-id="b2c2d-149">문자열</span><span class="sxs-lookup"><span data-stu-id="b2c2d-149">String</span></span>|<span data-ttu-id="b2c2d-150">hello의 hello 결과 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-150">hello result of hello resize.</span></span>|
|<span data-ttu-id="b2c2d-151">resultMessage</span><span class="sxs-lookup"><span data-stu-id="b2c2d-151">resultMessage</span></span>|<span data-ttu-id="b2c2d-152">문자열</span><span class="sxs-lookup"><span data-stu-id="b2c2d-152">String</span></span>|<span data-ttu-id="b2c2d-153">hello 크기 조정 오류 hello 결과의 hello 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-153">hello resize error includes hello details of hello result.</span></span><br /><br /> <span data-ttu-id="b2c2d-154">Hello 크기를 조정 하는 경우 성공적으로 완료 것 상태는 hello 작업에 성공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b2c2d-154">If hello resize completed successfully it states that hello operation succeeded.</span></span>|
