---
title: "Azure Batch 태스크 완료 이벤트 | Microsoft Docs"
description: "Batch 태스크 완료 이벤트에 대한 참조입니다."
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
ms.openlocfilehash: 015adf7dbc47c29a78df4e4889b2ee1ddcccdd8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="task-complete-event"></a><span data-ttu-id="7774d-103">태스크 완료 이벤트</span><span class="sxs-lookup"><span data-stu-id="7774d-103">Task complete event</span></span>

 <span data-ttu-id="7774d-104">이 이벤트는 종료 코드에 관계없이 태스크가 완료되면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-104">This event is emitted once a task is completed, regardless of the exit code.</span></span> <span data-ttu-id="7774d-105">이 이벤트는 태스크의 기간, 태스크가 실행된 위치 및 태스크가 재시도되었는지 여부를 확인하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-105">This event can be used to determine the duration of a task, where the task ran, and whether it was retried.</span></span>


 <span data-ttu-id="7774d-106">다음 예에서는 태스크 완료 이벤트의 본문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-106">The following example shows the body of a task complete event.</span></span>

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
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 0,
        "retryCount": 0,
        "requeueCount": 0
    }
}
```

|<span data-ttu-id="7774d-107">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7774d-107">Element name</span></span>|<span data-ttu-id="7774d-108">형식</span><span class="sxs-lookup"><span data-stu-id="7774d-108">Type</span></span>|<span data-ttu-id="7774d-109">참고 사항</span><span class="sxs-lookup"><span data-stu-id="7774d-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="7774d-110">jobId</span><span class="sxs-lookup"><span data-stu-id="7774d-110">jobId</span></span>|<span data-ttu-id="7774d-111">string</span><span class="sxs-lookup"><span data-stu-id="7774d-111">String</span></span>|<span data-ttu-id="7774d-112">태스크가 포함된 작업의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="7774d-113">id</span><span class="sxs-lookup"><span data-stu-id="7774d-113">id</span></span>|<span data-ttu-id="7774d-114">String</span><span class="sxs-lookup"><span data-stu-id="7774d-114">String</span></span>|<span data-ttu-id="7774d-115">태스크의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-115">The id of the task.</span></span>|
|<span data-ttu-id="7774d-116">taskType</span><span class="sxs-lookup"><span data-stu-id="7774d-116">taskType</span></span>|<span data-ttu-id="7774d-117">string</span><span class="sxs-lookup"><span data-stu-id="7774d-117">String</span></span>|<span data-ttu-id="7774d-118">태스크의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-118">The type of the task.</span></span> <span data-ttu-id="7774d-119">이는 작업 관리자 태스크를 나타내는 'JobManager' 또는 작업 관리자 태스크가 아님을 나타내는 'User'가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="7774d-120">작업 준비 태스크, 작업 릴리스 태스크 또는 시작 태스크의 경우 이 이벤트가 내보내지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-120">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="7774d-121">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="7774d-121">systemTaskVersion</span></span>|<span data-ttu-id="7774d-122">Int32</span><span class="sxs-lookup"><span data-stu-id="7774d-122">Int32</span></span>|<span data-ttu-id="7774d-123">태스크에 대한 내부 재시도 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-123">This is the internal retry counter on a task.</span></span> <span data-ttu-id="7774d-124">내부적으로 Batch 서비스는 일시적인 문제를 해결하기 위해 태스크를 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-124">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="7774d-125">이러한 문제에는 내부 일정 오류 또는 불량 상태의 계산 노드 복구를 위한 시도가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-125">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="7774d-126">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="7774d-126">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="7774d-127">복합 형식</span><span class="sxs-lookup"><span data-stu-id="7774d-127">Complex Type</span></span>|<span data-ttu-id="7774d-128">태스크가 실행된 계산 노드에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-128">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="7774d-129">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="7774d-129">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="7774d-130">복합 형식</span><span class="sxs-lookup"><span data-stu-id="7774d-130">Complex Type</span></span>|<span data-ttu-id="7774d-131">여러 계산 노드가 필요한 다중 인스턴스 태스크임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-131">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="7774d-132">자세한 내용은 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7774d-132">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="7774d-133">constraints</span><span class="sxs-lookup"><span data-stu-id="7774d-133">constraints</span></span>](#constraints)|<span data-ttu-id="7774d-134">복합 형식</span><span class="sxs-lookup"><span data-stu-id="7774d-134">Complex Type</span></span>|<span data-ttu-id="7774d-135">이 태스크에 적용되는 실행 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-135">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="7774d-136">executionInfo</span><span class="sxs-lookup"><span data-stu-id="7774d-136">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="7774d-137">복합 형식</span><span class="sxs-lookup"><span data-stu-id="7774d-137">Complex Type</span></span>|<span data-ttu-id="7774d-138">태스크 실행에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-138">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="7774d-139"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="7774d-139"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="7774d-140">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7774d-140">Element name</span></span>|<span data-ttu-id="7774d-141">형식</span><span class="sxs-lookup"><span data-stu-id="7774d-141">Type</span></span>|<span data-ttu-id="7774d-142">참고 사항</span><span class="sxs-lookup"><span data-stu-id="7774d-142">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="7774d-143">poolId</span><span class="sxs-lookup"><span data-stu-id="7774d-143">poolId</span></span>|<span data-ttu-id="7774d-144">String</span><span class="sxs-lookup"><span data-stu-id="7774d-144">String</span></span>|<span data-ttu-id="7774d-145">태스크가 실행된 풀의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-145">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="7774d-146">nodeId</span><span class="sxs-lookup"><span data-stu-id="7774d-146">nodeId</span></span>|<span data-ttu-id="7774d-147">string</span><span class="sxs-lookup"><span data-stu-id="7774d-147">String</span></span>|<span data-ttu-id="7774d-148">태스크가 실행된 노드의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-148">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="7774d-149"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="7774d-149"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="7774d-150">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7774d-150">Element name</span></span>|<span data-ttu-id="7774d-151">형식</span><span class="sxs-lookup"><span data-stu-id="7774d-151">Type</span></span>|<span data-ttu-id="7774d-152">참고 사항</span><span class="sxs-lookup"><span data-stu-id="7774d-152">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="7774d-153">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="7774d-153">numberOfInstances</span></span>|<span data-ttu-id="7774d-154">Int32</span><span class="sxs-lookup"><span data-stu-id="7774d-154">Int32</span></span>|<span data-ttu-id="7774d-155">태스크에 필요한 계산 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-155">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="7774d-156"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="7774d-156"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="7774d-157">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7774d-157">Element name</span></span>|<span data-ttu-id="7774d-158">형식</span><span class="sxs-lookup"><span data-stu-id="7774d-158">Type</span></span>|<span data-ttu-id="7774d-159">참고 사항</span><span class="sxs-lookup"><span data-stu-id="7774d-159">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="7774d-160">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="7774d-160">maxTaskRetryCount</span></span>|<span data-ttu-id="7774d-161">Int32</span><span class="sxs-lookup"><span data-stu-id="7774d-161">Int32</span></span>|<span data-ttu-id="7774d-162">태스크를 다시 시도할 수 있는 최대 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-162">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="7774d-163">종료 코드가 0이 아니면 Batch 서비스가 태스크를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-163">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="7774d-164">이 값은 구체적으로 재시도 횟수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-164">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="7774d-165">Batch 서비스는 태스크를 한 번 시도한 후 이 한도까지 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-165">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="7774d-166">예를 들어 최대 재시도 횟수가 3일 경우 Batch는 최대 4회까지 태스크를 시도합니다(초기 시도 1회와 재시도 3회).</span><span class="sxs-lookup"><span data-stu-id="7774d-166">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="7774d-167">최대 재시도 횟수가 0일 경우 Batch 서비스는 태스크를 다시 시도하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-167">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="7774d-168">최대 재시도 횟수가 -1일 경우 Batch 서비스는 태스크를 무제한으로 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-168">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="7774d-169">기본값은 0(재시도 안 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-169">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="7774d-170"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="7774d-170"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="7774d-171">요소 이름</span><span class="sxs-lookup"><span data-stu-id="7774d-171">Element name</span></span>|<span data-ttu-id="7774d-172">형식</span><span class="sxs-lookup"><span data-stu-id="7774d-172">Type</span></span>|<span data-ttu-id="7774d-173">참고 사항</span><span class="sxs-lookup"><span data-stu-id="7774d-173">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="7774d-174">startTime</span><span class="sxs-lookup"><span data-stu-id="7774d-174">startTime</span></span>|<span data-ttu-id="7774d-175">DateTime</span><span class="sxs-lookup"><span data-stu-id="7774d-175">DateTime</span></span>|<span data-ttu-id="7774d-176">태스크가 실행되기 시작한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-176">The time at which the task started running.</span></span> <span data-ttu-id="7774d-177">'Running'은 **실행 중** 상태에 해당하므로 태스크가 리소스 파일 또는 응용 프로그램 패키지를 지정할 경우 시작 시간에는 태스크가 이를 다운로드 또는 배포하기 시작한 시간이 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-177">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span></span>  <span data-ttu-id="7774d-178">태스크가 다시 시작되거나 다시 시도된 경우 이는 태스크가 실행을 시작한 가장 최근의 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-178">If the task has been restarted or retried, this is the most recent time at which the task started running.</span></span>|
|<span data-ttu-id="7774d-179">endTime</span><span class="sxs-lookup"><span data-stu-id="7774d-179">endTime</span></span>|<span data-ttu-id="7774d-180">DateTime</span><span class="sxs-lookup"><span data-stu-id="7774d-180">DateTime</span></span>|<span data-ttu-id="7774d-181">태스크가 완료된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-181">The time at which the task completed.</span></span>|
|<span data-ttu-id="7774d-182">exitCode</span><span class="sxs-lookup"><span data-stu-id="7774d-182">exitCode</span></span>|<span data-ttu-id="7774d-183">Int32</span><span class="sxs-lookup"><span data-stu-id="7774d-183">Int32</span></span>|<span data-ttu-id="7774d-184">태스크의 종료 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-184">The exit code of the task.</span></span>|
|<span data-ttu-id="7774d-185">retryCount</span><span class="sxs-lookup"><span data-stu-id="7774d-185">retryCount</span></span>|<span data-ttu-id="7774d-186">Int32</span><span class="sxs-lookup"><span data-stu-id="7774d-186">Int32</span></span>|<span data-ttu-id="7774d-187">Batch 서비스에서 태스크를 다시 시도한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-187">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="7774d-188">태스크가 0이 아닌 종료 코드와 함께 종료될 경우 지정된 MaxTaskRetryCount까지 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-188">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="7774d-189">requeueCount</span><span class="sxs-lookup"><span data-stu-id="7774d-189">requeueCount</span></span>|<span data-ttu-id="7774d-190">Int32</span><span class="sxs-lookup"><span data-stu-id="7774d-190">Int32</span></span>|<span data-ttu-id="7774d-191">사용자 요청으로 인해 Batch 서비스에서 태스크를 대기열에 다시 추가한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-191">The number of times the task has been requeued by the Batch service as the result of a user request.</span></span><br /><br /> <span data-ttu-id="7774d-192">사용자가 풀 크기 조정 또는 축소를 통해 풀에서 노드를 제거하거나 작업이 비활성화될 경우 사용자는 노드에서 실행 중인 태스크를 실행 대기열에 다시 추가하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-192">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span></span> <span data-ttu-id="7774d-193">이 개수는 태스크가 이러한 이유로 대기열에 다시 추가된 횟수를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="7774d-193">This count tracks how many times the task has been requeued for these reasons.</span></span>|
