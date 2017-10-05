---
title: "Azure Batch 태스크 실패 이벤트 | Microsoft Docs"
description: "Batch 태스크 실패 이벤트에 대한 참조입니다."
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
ms.openlocfilehash: 08feb4ec34bb1635f8ea744b54a10b677b94ab3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="task-fail-event"></a><span data-ttu-id="f7334-103">태스크 실패 이벤트</span><span class="sxs-lookup"><span data-stu-id="f7334-103">Task fail event</span></span>

 <span data-ttu-id="f7334-104">이 이벤트는 태스크가 오류와 함께 완료되면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-104">This event is emitted when a task completes with a failure.</span></span> <span data-ttu-id="f7334-105">현재 0이 아닌 종료 코드는 모두 오류로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-105">Currently all nonzero exit codes are considered failures.</span></span> <span data-ttu-id="f7334-106">이 이벤트는 태스크 완료 이벤트와 *별도로* 내보내지고, 태스크가 실패한 시기를 감지하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-106">This event will be emitted *in addition to* a task complete event and can be used to detect when a task has failed.</span></span>


 <span data-ttu-id="f7334-107">다음 예에서는 태스크 실패 이벤트의 본문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-107">The following example shows the body of a task fail event.</span></span>

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
        "exitCode": 1,
        "retryCount": 2,
        "requeueCount": 0
    }
}
```

|<span data-ttu-id="f7334-108">요소 이름</span><span class="sxs-lookup"><span data-stu-id="f7334-108">Element name</span></span>|<span data-ttu-id="f7334-109">형식</span><span class="sxs-lookup"><span data-stu-id="f7334-109">Type</span></span>|<span data-ttu-id="f7334-110">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f7334-110">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="f7334-111">jobId</span><span class="sxs-lookup"><span data-stu-id="f7334-111">jobId</span></span>|<span data-ttu-id="f7334-112">string</span><span class="sxs-lookup"><span data-stu-id="f7334-112">String</span></span>|<span data-ttu-id="f7334-113">태스크가 포함된 작업의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-113">The id of the job containing the task.</span></span>|
|<span data-ttu-id="f7334-114">id</span><span class="sxs-lookup"><span data-stu-id="f7334-114">id</span></span>|<span data-ttu-id="f7334-115">String</span><span class="sxs-lookup"><span data-stu-id="f7334-115">String</span></span>|<span data-ttu-id="f7334-116">태스크의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-116">The id of the task.</span></span>|
|<span data-ttu-id="f7334-117">taskType</span><span class="sxs-lookup"><span data-stu-id="f7334-117">taskType</span></span>|<span data-ttu-id="f7334-118">string</span><span class="sxs-lookup"><span data-stu-id="f7334-118">String</span></span>|<span data-ttu-id="f7334-119">태스크의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-119">The type of the task.</span></span> <span data-ttu-id="f7334-120">이는 작업 관리자 태스크를 나타내는 'JobManager' 또는 작업 관리자 태스크가 아님을 나타내는 'User'가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-120">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="f7334-121">작업 준비 태스크, 작업 릴리스 태스크 또는 시작 태스크의 경우 이 이벤트가 내보내지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-121">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="f7334-122">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="f7334-122">systemTaskVersion</span></span>|<span data-ttu-id="f7334-123">Int32</span><span class="sxs-lookup"><span data-stu-id="f7334-123">Int32</span></span>|<span data-ttu-id="f7334-124">태스크에 대한 내부 재시도 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-124">This is the internal retry counter on a task.</span></span> <span data-ttu-id="f7334-125">내부적으로 Batch 서비스는 일시적인 문제를 해결하기 위해 태스크를 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-125">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="f7334-126">이러한 문제에는 내부 일정 오류 또는 불량 상태의 계산 노드 복구를 위한 시도가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-126">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="f7334-127">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="f7334-127">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="f7334-128">복합 형식</span><span class="sxs-lookup"><span data-stu-id="f7334-128">Complex Type</span></span>|<span data-ttu-id="f7334-129">태스크가 실행된 계산 노드에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-129">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="f7334-130">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="f7334-130">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="f7334-131">복합 형식</span><span class="sxs-lookup"><span data-stu-id="f7334-131">Complex Type</span></span>|<span data-ttu-id="f7334-132">여러 계산 노드가 필요한 다중 인스턴스 태스크임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-132">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="f7334-133">자세한 내용은 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7334-133">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="f7334-134">constraints</span><span class="sxs-lookup"><span data-stu-id="f7334-134">constraints</span></span>](#constraints)|<span data-ttu-id="f7334-135">복합 형식</span><span class="sxs-lookup"><span data-stu-id="f7334-135">Complex Type</span></span>|<span data-ttu-id="f7334-136">이 태스크에 적용되는 실행 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-136">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="f7334-137">executionInfo</span><span class="sxs-lookup"><span data-stu-id="f7334-137">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="f7334-138">복합 형식</span><span class="sxs-lookup"><span data-stu-id="f7334-138">Complex Type</span></span>|<span data-ttu-id="f7334-139">태스크 실행에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-139">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="f7334-140"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="f7334-140"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="f7334-141">요소 이름</span><span class="sxs-lookup"><span data-stu-id="f7334-141">Element name</span></span>|<span data-ttu-id="f7334-142">형식</span><span class="sxs-lookup"><span data-stu-id="f7334-142">Type</span></span>|<span data-ttu-id="f7334-143">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f7334-143">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="f7334-144">poolId</span><span class="sxs-lookup"><span data-stu-id="f7334-144">poolId</span></span>|<span data-ttu-id="f7334-145">String</span><span class="sxs-lookup"><span data-stu-id="f7334-145">String</span></span>|<span data-ttu-id="f7334-146">태스크가 실행된 풀의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-146">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="f7334-147">nodeId</span><span class="sxs-lookup"><span data-stu-id="f7334-147">nodeId</span></span>|<span data-ttu-id="f7334-148">string</span><span class="sxs-lookup"><span data-stu-id="f7334-148">String</span></span>|<span data-ttu-id="f7334-149">태스크가 실행된 노드의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-149">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="f7334-150"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="f7334-150"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="f7334-151">요소 이름</span><span class="sxs-lookup"><span data-stu-id="f7334-151">Element name</span></span>|<span data-ttu-id="f7334-152">형식</span><span class="sxs-lookup"><span data-stu-id="f7334-152">Type</span></span>|<span data-ttu-id="f7334-153">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f7334-153">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="f7334-154">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="f7334-154">numberOfInstances</span></span>|<span data-ttu-id="f7334-155">Int32</span><span class="sxs-lookup"><span data-stu-id="f7334-155">Int32</span></span>|<span data-ttu-id="f7334-156">태스크에 필요한 계산 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-156">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="f7334-157"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="f7334-157"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="f7334-158">요소 이름</span><span class="sxs-lookup"><span data-stu-id="f7334-158">Element name</span></span>|<span data-ttu-id="f7334-159">형식</span><span class="sxs-lookup"><span data-stu-id="f7334-159">Type</span></span>|<span data-ttu-id="f7334-160">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f7334-160">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="f7334-161">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="f7334-161">maxTaskRetryCount</span></span>|<span data-ttu-id="f7334-162">Int32</span><span class="sxs-lookup"><span data-stu-id="f7334-162">Int32</span></span>|<span data-ttu-id="f7334-163">태스크를 다시 시도할 수 있는 최대 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-163">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="f7334-164">종료 코드가 0이 아니면 Batch 서비스가 태스크를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-164">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="f7334-165">이 값은 구체적으로 재시도 횟수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-165">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="f7334-166">Batch 서비스는 태스크를 한 번 시도한 후 이 한도까지 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-166">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="f7334-167">예를 들어 최대 재시도 횟수가 3일 경우 Batch는 최대 4회까지 태스크를 시도합니다(초기 시도 1회와 재시도 3회).</span><span class="sxs-lookup"><span data-stu-id="f7334-167">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="f7334-168">최대 재시도 횟수가 0일 경우 Batch 서비스는 태스크를 다시 시도하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-168">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="f7334-169">최대 재시도 횟수가 -1일 경우 Batch 서비스는 태스크를 무제한으로 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-169">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="f7334-170">기본값은 0(재시도 안 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-170">The default value is 0 (no retries).</span></span>|


###  <span data-ttu-id="f7334-171"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="f7334-171"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="f7334-172">요소 이름</span><span class="sxs-lookup"><span data-stu-id="f7334-172">Element name</span></span>|<span data-ttu-id="f7334-173">형식</span><span class="sxs-lookup"><span data-stu-id="f7334-173">Type</span></span>|<span data-ttu-id="f7334-174">참고 사항</span><span class="sxs-lookup"><span data-stu-id="f7334-174">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="f7334-175">startTime</span><span class="sxs-lookup"><span data-stu-id="f7334-175">startTime</span></span>|<span data-ttu-id="f7334-176">DateTime</span><span class="sxs-lookup"><span data-stu-id="f7334-176">DateTime</span></span>|<span data-ttu-id="f7334-177">태스크가 실행되기 시작한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-177">The time at which the task started running.</span></span> <span data-ttu-id="f7334-178">'Running'은 **실행 중** 상태에 해당하므로 태스크가 리소스 파일 또는 응용 프로그램 패키지를 지정할 경우 시작 시간에는 태스크가 이를 다운로드 또는 배포하기 시작한 시간이 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-178">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span></span>  <span data-ttu-id="f7334-179">태스크가 다시 시작되거나 다시 시도된 경우 이는 태스크가 실행을 시작한 가장 최근의 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-179">If the task has been restarted or retried, this is the most recent time at which the task started running.</span></span>|
|<span data-ttu-id="f7334-180">endTime</span><span class="sxs-lookup"><span data-stu-id="f7334-180">endTime</span></span>|<span data-ttu-id="f7334-181">DateTime</span><span class="sxs-lookup"><span data-stu-id="f7334-181">DateTime</span></span>|<span data-ttu-id="f7334-182">태스크가 완료된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-182">The time at which the task completed.</span></span>|
|<span data-ttu-id="f7334-183">exitCode</span><span class="sxs-lookup"><span data-stu-id="f7334-183">exitCode</span></span>|<span data-ttu-id="f7334-184">Int32</span><span class="sxs-lookup"><span data-stu-id="f7334-184">Int32</span></span>|<span data-ttu-id="f7334-185">태스크의 종료 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-185">The exit code of the task.</span></span>|
|<span data-ttu-id="f7334-186">retryCount</span><span class="sxs-lookup"><span data-stu-id="f7334-186">retryCount</span></span>|<span data-ttu-id="f7334-187">Int32</span><span class="sxs-lookup"><span data-stu-id="f7334-187">Int32</span></span>|<span data-ttu-id="f7334-188">Batch 서비스에서 태스크를 다시 시도한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-188">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="f7334-189">태스크가 0이 아닌 종료 코드와 함께 종료될 경우 지정된 MaxTaskRetryCount까지 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-189">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="f7334-190">requeueCount</span><span class="sxs-lookup"><span data-stu-id="f7334-190">requeueCount</span></span>|<span data-ttu-id="f7334-191">Int32</span><span class="sxs-lookup"><span data-stu-id="f7334-191">Int32</span></span>|<span data-ttu-id="f7334-192">사용자 요청으로 인해 Batch 서비스에서 태스크를 대기열에 다시 추가한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-192">The number of times the task has been requeued by the Batch service as the result of a user request.</span></span><br /><br /> <span data-ttu-id="f7334-193">사용자가 풀 크기 조정 또는 축소를 통해 풀에서 노드를 제거하거나 작업이 비활성화될 경우 사용자는 노드에서 실행 중인 태스크를 실행 대기열에 다시 추가하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-193">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span></span> <span data-ttu-id="f7334-194">이 개수는 태스크가 이러한 이유로 대기열에 다시 추가된 횟수를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="f7334-194">This count tracks how many times the task has been requeued for these reasons.</span></span>|
