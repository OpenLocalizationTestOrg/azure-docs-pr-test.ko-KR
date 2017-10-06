---
title: "aaa \"Azure 일괄 처리 작업 시작 이벤트 | \"Microsoft Docs"
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a><span data-ttu-id="1475e-103">태스크 시작 이벤트</span><span class="sxs-lookup"><span data-stu-id="1475e-103">Task start event</span></span>

 <span data-ttu-id="1475e-104">Hello 스케줄러에서 예약 된 toostart 계산 노드에서 작업 되 면이 이벤트가 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-104">This event is emitted once a task has been scheduled toostart on a compute node by hello scheduler.</span></span> <span data-ttu-id="1475e-105">Note는 hello 작업이 다시 시도 또는 다시 대기 하는 경우이 이벤트가 발생 다시 hello hello 하지만 같은 작업을 다시 시도 횟수와 시스템 태스크 버전을 적절 하 게 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-105">Note that if hello task is retried or requeued this event will be emitted again for hello same task, but hello retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="1475e-106">hello 다음 예제에서는 작업 시작 이벤트의 hello 본문</span><span class="sxs-lookup"><span data-stu-id="1475e-106">hello following example shows hello body of a task start event.</span></span>

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

|<span data-ttu-id="1475e-107">요소 이름</span><span class="sxs-lookup"><span data-stu-id="1475e-107">Element name</span></span>|<span data-ttu-id="1475e-108">형식</span><span class="sxs-lookup"><span data-stu-id="1475e-108">Type</span></span>|<span data-ttu-id="1475e-109">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1475e-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="1475e-110">jobId</span><span class="sxs-lookup"><span data-stu-id="1475e-110">jobId</span></span>|<span data-ttu-id="1475e-111">문자열</span><span class="sxs-lookup"><span data-stu-id="1475e-111">String</span></span>|<span data-ttu-id="1475e-112">hello 작업을 포함 하는 hello 작업의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="1475e-113">id</span><span class="sxs-lookup"><span data-stu-id="1475e-113">id</span></span>|<span data-ttu-id="1475e-114">문자열</span><span class="sxs-lookup"><span data-stu-id="1475e-114">String</span></span>|<span data-ttu-id="1475e-115">hello 작업의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-115">hello id of hello task.</span></span>|
|<span data-ttu-id="1475e-116">taskType</span><span class="sxs-lookup"><span data-stu-id="1475e-116">taskType</span></span>|<span data-ttu-id="1475e-117">문자열</span><span class="sxs-lookup"><span data-stu-id="1475e-117">String</span></span>|<span data-ttu-id="1475e-118">hello 작업의 hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-118">hello type of hello task.</span></span> <span data-ttu-id="1475e-119">이는 작업 관리자 태스크를 나타내는 'JobManager' 또는 작업 관리자 태스크가 아님을 나타내는 'User'가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="1475e-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="1475e-120">systemTaskVersion</span></span>|<span data-ttu-id="1475e-121">Int32</span><span class="sxs-lookup"><span data-stu-id="1475e-121">Int32</span></span>|<span data-ttu-id="1475e-122">작업에 내부 다시 시도 카운터가 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-122">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="1475e-123">내부적으로 hello 일괄 처리 서비스는 일시적인 문제에 대 한 작업 tooaccount 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-123">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="1475e-124">이러한 문제는 잘못 된 상태에 계산 노드 모두에서 내부 일정 오류나 시도 toorecover를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-124">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="1475e-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="1475e-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="1475e-126">복합 형식</span><span class="sxs-lookup"><span data-stu-id="1475e-126">Complex Type</span></span>|<span data-ttu-id="1475e-127">Hello 계산 노드는 hello 작업 실행에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-127">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="1475e-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="1475e-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="1475e-129">복합 형식</span><span class="sxs-lookup"><span data-stu-id="1475e-129">Complex Type</span></span>|<span data-ttu-id="1475e-130">해당 hello 작업은 여러 계산 노드를 요구 하는 다중 인스턴스 작업을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-130">Specifies that hello task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="1475e-131">자세한 내용은 [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1475e-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="1475e-132">constraints</span><span class="sxs-lookup"><span data-stu-id="1475e-132">constraints</span></span>](#constraints)|<span data-ttu-id="1475e-133">복합 형식</span><span class="sxs-lookup"><span data-stu-id="1475e-133">Complex Type</span></span>|<span data-ttu-id="1475e-134">hello 실행 적용 되는 제약 toothis 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-134">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="1475e-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="1475e-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="1475e-136">복합 형식</span><span class="sxs-lookup"><span data-stu-id="1475e-136">Complex Type</span></span>|<span data-ttu-id="1475e-137">Hello hello 작업 실행에 대 한 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-137">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="1475e-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="1475e-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="1475e-139">요소 이름</span><span class="sxs-lookup"><span data-stu-id="1475e-139">Element name</span></span>|<span data-ttu-id="1475e-140">형식</span><span class="sxs-lookup"><span data-stu-id="1475e-140">Type</span></span>|<span data-ttu-id="1475e-141">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1475e-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="1475e-142">poolId</span><span class="sxs-lookup"><span data-stu-id="1475e-142">poolId</span></span>|<span data-ttu-id="1475e-143">문자열</span><span class="sxs-lookup"><span data-stu-id="1475e-143">String</span></span>|<span data-ttu-id="1475e-144">태스크가 실행 하는 hello에 hello 풀의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-144">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="1475e-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="1475e-145">nodeId</span></span>|<span data-ttu-id="1475e-146">문자열</span><span class="sxs-lookup"><span data-stu-id="1475e-146">String</span></span>|<span data-ttu-id="1475e-147">태스크가 실행 하는 hello에 hello 노드의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-147">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="1475e-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="1475e-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="1475e-149">요소 이름</span><span class="sxs-lookup"><span data-stu-id="1475e-149">Element name</span></span>|<span data-ttu-id="1475e-150">형식</span><span class="sxs-lookup"><span data-stu-id="1475e-150">Type</span></span>|<span data-ttu-id="1475e-151">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1475e-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="1475e-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="1475e-152">numberOfInstances</span></span>|<span data-ttu-id="1475e-153">int</span><span class="sxs-lookup"><span data-stu-id="1475e-153">Int</span></span>|<span data-ttu-id="1475e-154">hello hello 작업에 필요한 하는 계산 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-154">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="1475e-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="1475e-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="1475e-156">요소 이름</span><span class="sxs-lookup"><span data-stu-id="1475e-156">Element name</span></span>|<span data-ttu-id="1475e-157">형식</span><span class="sxs-lookup"><span data-stu-id="1475e-157">Type</span></span>|<span data-ttu-id="1475e-158">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1475e-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="1475e-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="1475e-159">maxTaskRetryCount</span></span>|<span data-ttu-id="1475e-160">Int32</span><span class="sxs-lookup"><span data-stu-id="1475e-160">Int32</span></span>|<span data-ttu-id="1475e-161">hello 최대 횟수 hello 작업을 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-161">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="1475e-162">종료 코드가 0이 아니면 hello 일괄 처리 서비스는 작업을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-162">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="1475e-163">이 값 hello 재시도 횟수를 구체적으로 제어 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-163">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="1475e-164">hello 일괄 처리 서비스 hello 작업을 한 번 시도 합니다 및 toothis 한도를 다음 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-164">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="1475e-165">예를 들어 hello 최대 다시 시도 횟수는 3, 일괄 처리 (한 번의 초기 시도 및 3 회) 시간 too4 구성 작업을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-165">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="1475e-166">Hello 최대 다시 시도 횟수가 0 인 경우 hello 일괄 처리 서비스 작업을 재시도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-166">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="1475e-167">Hello 최대 다시 시도 횟수가-1 이면 hello 일괄 처리 서비스가 작업 제한 없이 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-167">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="1475e-168">hello 기본값은 0 (다시 시도 안 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-168">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="1475e-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="1475e-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="1475e-170">요소 이름</span><span class="sxs-lookup"><span data-stu-id="1475e-170">Element name</span></span>|<span data-ttu-id="1475e-171">형식</span><span class="sxs-lookup"><span data-stu-id="1475e-171">Type</span></span>|<span data-ttu-id="1475e-172">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1475e-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="1475e-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="1475e-173">retryCount</span></span>|<span data-ttu-id="1475e-174">Int32</span><span class="sxs-lookup"><span data-stu-id="1475e-174">Int32</span></span>|<span data-ttu-id="1475e-175">hello hello 작업 hello 일괄 처리 서비스에서 다시 시도한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="1475e-175">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="1475e-176">지정 된 MaxTaskRetryCount toohello를 0이 아닌 종료 코드로 종료 hello 작업을 다시 시도</span><span class="sxs-lookup"><span data-stu-id="1475e-176">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount</span></span>|
