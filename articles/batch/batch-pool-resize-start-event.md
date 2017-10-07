---
title: "aaa \"Azure 배치 풀 크기 조정 이벤트를 시작 | \"Microsoft Docs"
description: "Batch 풀 크기 조정 시작 이벤트에 대한 참조입니다."
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="85e20-103">풀 크기 조정 시작 이벤트</span><span class="sxs-lookup"><span data-stu-id="85e20-103">Pool resize start event</span></span>

 <span data-ttu-id="85e20-104">이 이벤트는 풀 크기 조정이 시작되면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="85e20-105">Hello 풀 크기 조정 비동기 이벤트 이므로 hello 크기 조정 작업 후 발생 하는 풀 크기 조정 완료 이벤트 toobe 완료 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-105">Since hello pool resize is an asynchronous event, you can expect a pool resize complete event toobe emitted once hello resize operation completes.</span></span>

 <span data-ttu-id="85e20-106">다음 예제에서는 수동으로 too2 노드 모두 0에서 풀 크기에 대 한 풀 크기 조정 시작 이벤트의 본문 hello hello 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-106">hello following example shows hello body of a pool resize start event for a pool resizing from 0 too2 nodes with a manual resize.</span></span>

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|<span data-ttu-id="85e20-107">요소</span><span class="sxs-lookup"><span data-stu-id="85e20-107">Element</span></span>|<span data-ttu-id="85e20-108">형식</span><span class="sxs-lookup"><span data-stu-id="85e20-108">Type</span></span>|<span data-ttu-id="85e20-109">참고 사항</span><span class="sxs-lookup"><span data-stu-id="85e20-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="85e20-110">poolId</span><span class="sxs-lookup"><span data-stu-id="85e20-110">poolId</span></span>|<span data-ttu-id="85e20-111">문자열</span><span class="sxs-lookup"><span data-stu-id="85e20-111">String</span></span>|<span data-ttu-id="85e20-112">hello 풀의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-112">hello id of hello pool.</span></span>|
|<span data-ttu-id="85e20-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="85e20-113">nodeDeallocationOption</span></span>|<span data-ttu-id="85e20-114">문자열</span><span class="sxs-lookup"><span data-stu-id="85e20-114">String</span></span>|<span data-ttu-id="85e20-115">Hello 풀 크기가 감소 하는 경우 노드 hello 풀에서 제거할 수 있는 시기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-115">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="85e20-116">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="85e20-117">**requeue** – 실행 중인 태스크를 종료하고 해당 태스크를 다시 대기열에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="85e20-118">hello 작업이 사용 되는지 hello 작업 다시 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-118">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="85e20-119">태스크가 종료되는 즉시 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="85e20-120">**terminate** – 실행 중인 태스크를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="85e20-121">hello 작업 다시 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-121">hello tasks will not run again.</span></span> <span data-ttu-id="85e20-122">태스크가 종료되는 즉시 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="85e20-123">**taskcompletion** – 현재 작업 toocomplete 실행 되 고 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-123">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="85e20-124">대기하는 동안 새 태스크를 예약하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="85e20-125">모든 태스크가 완료되면 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="85e20-126">**Retaineddata** -현재 실행 되는 작업 toocomplete을 모든 작업 데이터 보존 기간 tooexpire 기다리세요.</span><span class="sxs-lookup"><span data-stu-id="85e20-126">**Retaineddata** - Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="85e20-127">대기하는 동안 새 태스크를 예약하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="85e20-128">모든 태스크 보존 기간이 만료되면 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="85e20-129">hello 기본값은 큐에 다시 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-129">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="85e20-130">Hello 풀 크기가 계속 증가 하는 경우 hello 값이 너무 설정**잘못 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-130">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="85e20-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="85e20-131">currentDedicated</span></span>|<span data-ttu-id="85e20-132">Int32</span><span class="sxs-lookup"><span data-stu-id="85e20-132">Int32</span></span>|<span data-ttu-id="85e20-133">hello 계산 노드 수는 현재 toohello 풀을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-133">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="85e20-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="85e20-134">targetDedicated</span></span>|<span data-ttu-id="85e20-135">Int32</span><span class="sxs-lookup"><span data-stu-id="85e20-135">Int32</span></span>|<span data-ttu-id="85e20-136">hello hello 풀에 대해 요청 된 계산 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-136">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="85e20-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="85e20-137">enableAutoScale</span></span>|<span data-ttu-id="85e20-138">Bool</span><span class="sxs-lookup"><span data-stu-id="85e20-138">Bool</span></span>|<span data-ttu-id="85e20-139">Hello 풀 크기 시간에 따라 자동으로 조정 되는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e20-139">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="85e20-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="85e20-140">isAutoPool</span></span>|<span data-ttu-id="85e20-141">Bool</span><span class="sxs-lookup"><span data-stu-id="85e20-141">Bool</span></span>|<span data-ttu-id="85e20-142">지정 hello 풀 작업의 자동 풀 메커니즘을 통해 생성 된 여부.</span><span class="sxs-lookup"><span data-stu-id="85e20-142">Speficies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
