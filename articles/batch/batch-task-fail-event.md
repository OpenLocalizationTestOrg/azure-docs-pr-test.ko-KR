---
title: "aaa \"Azure 일괄 처리 작업 실패 이벤트 | \"Microsoft Docs"
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
ms.openlocfilehash: e92604671650900072ba27f807501b704329e865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="task-fail-event"></a><span data-ttu-id="c58cc-103">태스크 실패 이벤트</span><span class="sxs-lookup"><span data-stu-id="c58cc-103">Task fail event</span></span>

 <span data-ttu-id="c58cc-104">이 이벤트는 태스크가 오류와 함께 완료되면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-104">This event is emitted when a task completes with a failure.</span></span> <span data-ttu-id="c58cc-105">현재 0이 아닌 종료 코드는 모두 오류로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-105">Currently all nonzero exit codes are considered failures.</span></span> <span data-ttu-id="c58cc-106">이 이벤트는 발생 *외에* 작업 이벤트를 완료 하 고 작업에 실패 한 경우 사용 되는 toodetect 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-106">This event will be emitted *in addition to* a task complete event and can be used toodetect when a task has failed.</span></span>


 <span data-ttu-id="c58cc-107">hello 다음 예제에서는 작업의 본문 hello 실패 이벤트</span><span class="sxs-lookup"><span data-stu-id="c58cc-107">hello following example shows hello body of a task fail event.</span></span>

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

|<span data-ttu-id="c58cc-108">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c58cc-108">Element name</span></span>|<span data-ttu-id="c58cc-109">형식</span><span class="sxs-lookup"><span data-stu-id="c58cc-109">Type</span></span>|<span data-ttu-id="c58cc-110">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c58cc-110">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="c58cc-111">jobId</span><span class="sxs-lookup"><span data-stu-id="c58cc-111">jobId</span></span>|<span data-ttu-id="c58cc-112">문자열</span><span class="sxs-lookup"><span data-stu-id="c58cc-112">String</span></span>|<span data-ttu-id="c58cc-113">hello 작업을 포함 하는 hello 작업의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-113">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="c58cc-114">id</span><span class="sxs-lookup"><span data-stu-id="c58cc-114">id</span></span>|<span data-ttu-id="c58cc-115">문자열</span><span class="sxs-lookup"><span data-stu-id="c58cc-115">String</span></span>|<span data-ttu-id="c58cc-116">hello 작업의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-116">hello id of hello task.</span></span>|
|<span data-ttu-id="c58cc-117">taskType</span><span class="sxs-lookup"><span data-stu-id="c58cc-117">taskType</span></span>|<span data-ttu-id="c58cc-118">문자열</span><span class="sxs-lookup"><span data-stu-id="c58cc-118">String</span></span>|<span data-ttu-id="c58cc-119">hello 작업의 hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-119">hello type of hello task.</span></span> <span data-ttu-id="c58cc-120">이는 작업 관리자 태스크를 나타내는 'JobManager' 또는 작업 관리자 태스크가 아님을 나타내는 'User'가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-120">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="c58cc-121">작업 준비 태스크, 작업 릴리스 태스크 또는 시작 태스크의 경우 이 이벤트가 내보내지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-121">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="c58cc-122">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="c58cc-122">systemTaskVersion</span></span>|<span data-ttu-id="c58cc-123">Int32</span><span class="sxs-lookup"><span data-stu-id="c58cc-123">Int32</span></span>|<span data-ttu-id="c58cc-124">작업에 내부 다시 시도 카운터가 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-124">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="c58cc-125">내부적으로 hello 일괄 처리 서비스는 일시적인 문제에 대 한 작업 tooaccount 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-125">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="c58cc-126">이러한 문제는 잘못 된 상태에 계산 노드 모두에서 내부 일정 오류나 시도 toorecover를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-126">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="c58cc-127">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="c58cc-127">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="c58cc-128">복합 형식</span><span class="sxs-lookup"><span data-stu-id="c58cc-128">Complex Type</span></span>|<span data-ttu-id="c58cc-129">Hello 계산 노드는 hello 작업 실행에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-129">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="c58cc-130">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="c58cc-130">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="c58cc-131">복합 형식</span><span class="sxs-lookup"><span data-stu-id="c58cc-131">Complex Type</span></span>|<span data-ttu-id="c58cc-132">해당 hello 작업은 여러 계산 노드를 요구 하는 다중 인스턴스 작업을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-132">Specifies that hello task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="c58cc-133">자세한 내용은 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c58cc-133">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="c58cc-134">constraints</span><span class="sxs-lookup"><span data-stu-id="c58cc-134">constraints</span></span>](#constraints)|<span data-ttu-id="c58cc-135">복합 형식</span><span class="sxs-lookup"><span data-stu-id="c58cc-135">Complex Type</span></span>|<span data-ttu-id="c58cc-136">hello 실행 적용 되는 제약 toothis 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-136">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="c58cc-137">executionInfo</span><span class="sxs-lookup"><span data-stu-id="c58cc-137">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="c58cc-138">복합 형식</span><span class="sxs-lookup"><span data-stu-id="c58cc-138">Complex Type</span></span>|<span data-ttu-id="c58cc-139">Hello hello 작업 실행에 대 한 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-139">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="c58cc-140"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="c58cc-140"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="c58cc-141">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c58cc-141">Element name</span></span>|<span data-ttu-id="c58cc-142">형식</span><span class="sxs-lookup"><span data-stu-id="c58cc-142">Type</span></span>|<span data-ttu-id="c58cc-143">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c58cc-143">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="c58cc-144">poolId</span><span class="sxs-lookup"><span data-stu-id="c58cc-144">poolId</span></span>|<span data-ttu-id="c58cc-145">문자열</span><span class="sxs-lookup"><span data-stu-id="c58cc-145">String</span></span>|<span data-ttu-id="c58cc-146">태스크가 실행 하는 hello에 hello 풀의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-146">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="c58cc-147">nodeId</span><span class="sxs-lookup"><span data-stu-id="c58cc-147">nodeId</span></span>|<span data-ttu-id="c58cc-148">문자열</span><span class="sxs-lookup"><span data-stu-id="c58cc-148">String</span></span>|<span data-ttu-id="c58cc-149">태스크가 실행 하는 hello에 hello 노드의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-149">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="c58cc-150"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="c58cc-150"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="c58cc-151">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c58cc-151">Element name</span></span>|<span data-ttu-id="c58cc-152">형식</span><span class="sxs-lookup"><span data-stu-id="c58cc-152">Type</span></span>|<span data-ttu-id="c58cc-153">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c58cc-153">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="c58cc-154">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="c58cc-154">numberOfInstances</span></span>|<span data-ttu-id="c58cc-155">Int32</span><span class="sxs-lookup"><span data-stu-id="c58cc-155">Int32</span></span>|<span data-ttu-id="c58cc-156">hello hello 작업에 필요한 하는 계산 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-156">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="c58cc-157"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="c58cc-157"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="c58cc-158">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c58cc-158">Element name</span></span>|<span data-ttu-id="c58cc-159">형식</span><span class="sxs-lookup"><span data-stu-id="c58cc-159">Type</span></span>|<span data-ttu-id="c58cc-160">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c58cc-160">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="c58cc-161">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="c58cc-161">maxTaskRetryCount</span></span>|<span data-ttu-id="c58cc-162">Int32</span><span class="sxs-lookup"><span data-stu-id="c58cc-162">Int32</span></span>|<span data-ttu-id="c58cc-163">hello 최대 횟수 hello 작업을 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-163">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="c58cc-164">종료 코드가 0이 아니면 hello 일괄 처리 서비스는 작업을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-164">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="c58cc-165">이 값 hello 재시도 횟수를 구체적으로 제어 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-165">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="c58cc-166">hello 일괄 처리 서비스 hello 작업을 한 번 시도 합니다 및 toothis 한도를 다음 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-166">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="c58cc-167">예를 들어 hello 최대 다시 시도 횟수는 3, 일괄 처리 (한 번의 초기 시도 및 3 회) 시간 too4 구성 작업을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-167">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="c58cc-168">Hello 최대 다시 시도 횟수가 0 인 경우 hello 일괄 처리 서비스 작업을 재시도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-168">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="c58cc-169">Hello 최대 다시 시도 횟수가-1 이면 hello 일괄 처리 서비스가 작업 제한 없이 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-169">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="c58cc-170">hello 기본값은 0 (다시 시도 안 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-170">hello default value is 0 (no retries).</span></span>|


###  <span data-ttu-id="c58cc-171"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="c58cc-171"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="c58cc-172">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c58cc-172">Element name</span></span>|<span data-ttu-id="c58cc-173">형식</span><span class="sxs-lookup"><span data-stu-id="c58cc-173">Type</span></span>|<span data-ttu-id="c58cc-174">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c58cc-174">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="c58cc-175">startTime</span><span class="sxs-lookup"><span data-stu-id="c58cc-175">startTime</span></span>|<span data-ttu-id="c58cc-176">DateTime</span><span class="sxs-lookup"><span data-stu-id="c58cc-176">DateTime</span></span>|<span data-ttu-id="c58cc-177">hello 작업 실행이 시작 시 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-177">hello time at which hello task started running.</span></span> <span data-ttu-id="c58cc-178">Toohello 해당 '실행 중' **실행** 상태 이면 나타내도록 hello 작업에서 리소스 파일 또는 응용 프로그램 패키지를 지정 하는 경우 다음 hello 시작 시간 hello 시간 다운로드 하거나 배포를 시작 하는 hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-178">'Running' corresponds toohello **running** state, so if hello task specifies resource files or application packages, then hello start time reflects hello time at which hello task started downloading or deploying these.</span></span>  <span data-ttu-id="c58cc-179">Hello 작업 다시 시작 되거나 다시 시도 된 경우이 hello 실행이 시작 되는 hello 작업에 대 한 가장 최근 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-179">If hello task has been restarted or retried, this is hello most recent time at which hello task started running.</span></span>|
|<span data-ttu-id="c58cc-180">endTime</span><span class="sxs-lookup"><span data-stu-id="c58cc-180">endTime</span></span>|<span data-ttu-id="c58cc-181">DateTime</span><span class="sxs-lookup"><span data-stu-id="c58cc-181">DateTime</span></span>|<span data-ttu-id="c58cc-182">hello 시기는 hello 작업이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-182">hello time at which hello task completed.</span></span>|
|<span data-ttu-id="c58cc-183">exitCode</span><span class="sxs-lookup"><span data-stu-id="c58cc-183">exitCode</span></span>|<span data-ttu-id="c58cc-184">Int32</span><span class="sxs-lookup"><span data-stu-id="c58cc-184">Int32</span></span>|<span data-ttu-id="c58cc-185">hello hello 작업의 종료 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-185">hello exit code of hello task.</span></span>|
|<span data-ttu-id="c58cc-186">retryCount</span><span class="sxs-lookup"><span data-stu-id="c58cc-186">retryCount</span></span>|<span data-ttu-id="c58cc-187">Int32</span><span class="sxs-lookup"><span data-stu-id="c58cc-187">Int32</span></span>|<span data-ttu-id="c58cc-188">hello hello 작업 hello 일괄 처리 서비스에서 다시 시도한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-188">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="c58cc-189">지정 된 MaxTaskRetryCount toohello를 0이 아닌 종료 코드로 종료 하는 경우에 hello 태스크를 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-189">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="c58cc-190">requeueCount</span><span class="sxs-lookup"><span data-stu-id="c58cc-190">requeueCount</span></span>|<span data-ttu-id="c58cc-191">Int32</span><span class="sxs-lookup"><span data-stu-id="c58cc-191">Int32</span></span>|<span data-ttu-id="c58cc-192">hello hello 작업이 다시 대기 hello 일괄 처리 서비스에서 사용자 요청의 hello 결과로 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-192">hello number of times hello task has been requeued by hello Batch service as hello result of a user request.</span></span><br /><br /> <span data-ttu-id="c58cc-193">때 실행을 위해 다시 대기열에 hello 사용자 제거 (하 여 hello 풀 축소) 풀 또는 hello 작업이 해제 되는 경우, hello 사용자에서 노드 hello 노드에서 실행 중인 작업을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-193">When hello user removes nodes from a pool (by resizing or shrinking hello pool) or when hello job is being disabled, hello user can specify that running tasks on hello nodes be requeued for execution.</span></span> <span data-ttu-id="c58cc-194">이 개수 이러한 이유로 몇 번 hello 작업을 다시 대기를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="c58cc-194">This count tracks how many times hello task has been requeued for these reasons.</span></span>|
