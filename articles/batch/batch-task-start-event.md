---
title: "Azure Batch 태스크 시작 이벤트 | Microsoft Docs"
description: "Batch 태스크 시작 이벤트에 대한 참조입니다."
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
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a><span data-ttu-id="ed79b-103">태스크 시작 이벤트</span><span class="sxs-lookup"><span data-stu-id="ed79b-103">Task start event</span></span>

 <span data-ttu-id="ed79b-104">이 이벤트는 Scheduler가 계산 노드에서 태스크를 시작하도록 예약하면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="ed79b-105">태스크가 다시 시도되거나 대기열에 다시 추가될 경우 동일한 태스크에 이 이벤트가 다시 내보내지지만 재시도 횟수와 시스템 태스크 버전이 적절히 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="ed79b-106">다음 예에서는 태스크 시작 이벤트의 본문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-106">The following example shows the body of a task start event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|<span data-ttu-id="ed79b-107">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ed79b-107">Element name</span></span>|<span data-ttu-id="ed79b-108">형식</span><span class="sxs-lookup"><span data-stu-id="ed79b-108">Type</span></span>|<span data-ttu-id="ed79b-109">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ed79b-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="ed79b-110">jobId</span><span class="sxs-lookup"><span data-stu-id="ed79b-110">jobId</span></span>|<span data-ttu-id="ed79b-111">string</span><span class="sxs-lookup"><span data-stu-id="ed79b-111">String</span></span>|<span data-ttu-id="ed79b-112">태스크가 포함된 작업의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="ed79b-113">id</span><span class="sxs-lookup"><span data-stu-id="ed79b-113">id</span></span>|<span data-ttu-id="ed79b-114">String</span><span class="sxs-lookup"><span data-stu-id="ed79b-114">String</span></span>|<span data-ttu-id="ed79b-115">태스크의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-115">The id of the task.</span></span>|
|<span data-ttu-id="ed79b-116">taskType</span><span class="sxs-lookup"><span data-stu-id="ed79b-116">taskType</span></span>|<span data-ttu-id="ed79b-117">string</span><span class="sxs-lookup"><span data-stu-id="ed79b-117">String</span></span>|<span data-ttu-id="ed79b-118">태스크의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-118">The type of the task.</span></span> <span data-ttu-id="ed79b-119">이는 작업 관리자 태스크를 나타내는 'JobManager' 또는 작업 관리자 태스크가 아님을 나타내는 'User'가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="ed79b-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="ed79b-120">systemTaskVersion</span></span>|<span data-ttu-id="ed79b-121">Int32</span><span class="sxs-lookup"><span data-stu-id="ed79b-121">Int32</span></span>|<span data-ttu-id="ed79b-122">태스크에 대한 내부 재시도 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="ed79b-123">내부적으로 Batch 서비스는 일시적인 문제를 해결하기 위해 태스크를 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="ed79b-124">이러한 문제에는 내부 일정 오류 또는 불량 상태의 계산 노드 복구를 위한 시도가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="ed79b-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="ed79b-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="ed79b-126">복합 형식</span><span class="sxs-lookup"><span data-stu-id="ed79b-126">Complex Type</span></span>|<span data-ttu-id="ed79b-127">태스크가 실행된 계산 노드에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="ed79b-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="ed79b-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="ed79b-129">복합 형식</span><span class="sxs-lookup"><span data-stu-id="ed79b-129">Complex Type</span></span>|<span data-ttu-id="ed79b-130">여러 계산 노드가 필요한 다중 인스턴스 태스크임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="ed79b-131">자세한 내용은 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed79b-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="ed79b-132">constraints</span><span class="sxs-lookup"><span data-stu-id="ed79b-132">constraints</span></span>](#constraints)|<span data-ttu-id="ed79b-133">복합 형식</span><span class="sxs-lookup"><span data-stu-id="ed79b-133">Complex Type</span></span>|<span data-ttu-id="ed79b-134">이 태스크에 적용되는 실행 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="ed79b-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="ed79b-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="ed79b-136">복합 형식</span><span class="sxs-lookup"><span data-stu-id="ed79b-136">Complex Type</span></span>|<span data-ttu-id="ed79b-137">태스크 실행에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-137">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="ed79b-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="ed79b-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="ed79b-139">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ed79b-139">Element name</span></span>|<span data-ttu-id="ed79b-140">형식</span><span class="sxs-lookup"><span data-stu-id="ed79b-140">Type</span></span>|<span data-ttu-id="ed79b-141">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ed79b-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="ed79b-142">poolId</span><span class="sxs-lookup"><span data-stu-id="ed79b-142">poolId</span></span>|<span data-ttu-id="ed79b-143">String</span><span class="sxs-lookup"><span data-stu-id="ed79b-143">String</span></span>|<span data-ttu-id="ed79b-144">태스크가 실행된 풀의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="ed79b-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="ed79b-145">nodeId</span></span>|<span data-ttu-id="ed79b-146">string</span><span class="sxs-lookup"><span data-stu-id="ed79b-146">String</span></span>|<span data-ttu-id="ed79b-147">태스크가 실행된 노드의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-147">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="ed79b-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="ed79b-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="ed79b-149">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ed79b-149">Element name</span></span>|<span data-ttu-id="ed79b-150">형식</span><span class="sxs-lookup"><span data-stu-id="ed79b-150">Type</span></span>|<span data-ttu-id="ed79b-151">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ed79b-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="ed79b-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="ed79b-152">numberOfInstances</span></span>|<span data-ttu-id="ed79b-153">int</span><span class="sxs-lookup"><span data-stu-id="ed79b-153">Int</span></span>|<span data-ttu-id="ed79b-154">태스크에 필요한 계산 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-154">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="ed79b-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="ed79b-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="ed79b-156">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ed79b-156">Element name</span></span>|<span data-ttu-id="ed79b-157">형식</span><span class="sxs-lookup"><span data-stu-id="ed79b-157">Type</span></span>|<span data-ttu-id="ed79b-158">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ed79b-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="ed79b-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="ed79b-159">maxTaskRetryCount</span></span>|<span data-ttu-id="ed79b-160">Int32</span><span class="sxs-lookup"><span data-stu-id="ed79b-160">Int32</span></span>|<span data-ttu-id="ed79b-161">태스크를 다시 시도할 수 있는 최대 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="ed79b-162">종료 코드가 0이 아니면 Batch 서비스가 태스크를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="ed79b-163">이 값은 구체적으로 재시도 횟수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="ed79b-164">Batch 서비스는 태스크를 한 번 시도한 후 이 한도까지 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="ed79b-165">예를 들어 최대 재시도 횟수가 3일 경우 Batch는 최대 4회까지 태스크를 시도합니다(초기 시도 1회와 재시도 3회).</span><span class="sxs-lookup"><span data-stu-id="ed79b-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="ed79b-166">최대 재시도 횟수가 0일 경우 Batch 서비스는 태스크를 다시 시도하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="ed79b-167">최대 재시도 횟수가 -1일 경우 Batch 서비스는 태스크를 무제한으로 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="ed79b-168">기본값은 0(재시도 안 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-168">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="ed79b-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="ed79b-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="ed79b-170">요소 이름</span><span class="sxs-lookup"><span data-stu-id="ed79b-170">Element name</span></span>|<span data-ttu-id="ed79b-171">형식</span><span class="sxs-lookup"><span data-stu-id="ed79b-171">Type</span></span>|<span data-ttu-id="ed79b-172">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ed79b-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="ed79b-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="ed79b-173">retryCount</span></span>|<span data-ttu-id="ed79b-174">Int32</span><span class="sxs-lookup"><span data-stu-id="ed79b-174">Int32</span></span>|<span data-ttu-id="ed79b-175">Batch 서비스에서 태스크를 다시 시도한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="ed79b-176">태스크가 0이 아닌 종료 코드와 함께 종료될 경우 지정된 MaxTaskRetryCount까지 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed79b-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
