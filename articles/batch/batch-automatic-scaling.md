---
title: "aaaAutomatically 눈금의에서 계산 노드 Azure 배치 풀 | Microsoft Docs"
description: "Enable에 대해 자동 크기 조정을 클라우드 풀 toodynamically hello hello 풀의 계산 노드 수를 조정 합니다."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a><span data-ttu-id="b9713-103">Batch 풀에서 계산 노드의 크기를 조정하는 자동 크기 조정 수식 만들기</span><span class="sxs-lookup"><span data-stu-id="b9713-103">Create an automatic scaling formula for scaling compute nodes in a Batch pool</span></span>

<span data-ttu-id="b9713-104">Azure Batch는 정의한 매개 변수에 따라 풀을 자동으로 크기 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-104">Azure Batch can automatically scale pools based on parameters that you define.</span></span> <span data-ttu-id="b9713-105">자동 크기 조정 된 일괄 처리 작업 요구량이 증가으로 노드 tooa 풀을 동적으로 추가 및 감소은 계산 노드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-105">With automatic scaling, Batch dynamically adds nodes tooa pool as task demands increase, and removes compute nodes as they decrease.</span></span> <span data-ttu-id="b9713-106">Hello 일괄 처리 응용 프로그램에서 사용 되는 계산 노드 수를 자동으로 조정 하 여 시간과 비용을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-106">You can save both time and money by automatically adjusting hello number of compute nodes used by your Batch application.</span></span> 

<span data-ttu-id="b9713-107">사용자가 정의한 *자동 크기 조정 수식*에 연결하면 계산 노드 풀에서 자동으로 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-107">You enable automatic scaling on a pool of compute nodes by associating with it an *autoscale formula* that you define.</span></span> <span data-ttu-id="b9713-108">hello 일괄 처리 서비스는 hello 자동 크기 조정 수식 toodetermine hello 계산 노드 수를 필요한 tooexecute는 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-108">hello Batch service uses hello autoscale formula toodetermine hello number of compute nodes that are needed tooexecute your workload.</span></span> <span data-ttu-id="b9713-109">계산 노드는 전용 노드이거나 [우선 순위가 낮은 노드](batch-low-pri-vms.md)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-109">Compute nodes may be dedicated nodes or [low-priority nodes](batch-low-pri-vms.md).</span></span> <span data-ttu-id="b9713-110">일괄 처리 응답 tooservice 메트릭 데이터는 주기적으로 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-110">Batch responds tooservice metrics data that is collected periodically.</span></span> <span data-ttu-id="b9713-111">이 메트릭 데이터를 사용 하 여 일괄 처리는 hello 수식에서 구성 가능한 간격을 기반으로 하는 hello 풀의 계산 노드 수를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-111">Using this metrics data, Batch adjusts hello number of compute nodes in hello pool based on your formula and at a configurable interval.</span></span>

<span data-ttu-id="b9713-112">풀을 만들 때 또는 기존 풀에서 자동 크기 조정을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-112">You can enable automatic scaling either when a pool is created, or on an existing pool.</span></span> <span data-ttu-id="b9713-113">자동 크기 조정에 대해 구성된 풀의 기존 수식을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-113">You can also change an existing formula on a pool that is configured for autoscaling.</span></span> <span data-ttu-id="b9713-114">일괄 처리에 자동 크기 조정의 toopools 및 toomonitor hello 상태를 할당 하기 전에 수식을 실행 tooevaluate가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-114">Batch enables you tooevaluate your formulas before assigning them toopools and toomonitor hello status of automatic scaling runs.</span></span>

<span data-ttu-id="b9713-115">이 문서에서는 hello, 변수, 연산자, 작업 및 함수를 포함 하 여 자동 크기 조정 수식을 구성 하는 다양 한 엔터티.</span><span class="sxs-lookup"><span data-stu-id="b9713-115">This article discusses hello various entities that make up your autoscale formulas, including variables, operators, operations, and functions.</span></span> <span data-ttu-id="b9713-116">에서는 어떻게 tooobtain 다양 한 일괄 처리 내에서 리소스 및 작업 메트릭을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-116">We discuss how tooobtain various compute resource and task metrics within Batch.</span></span> <span data-ttu-id="b9713-117">이러한 메트릭을 tooadjust 리소스 사용량 및 작업 상태에 따라 풀의 노드 수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-117">You can use these metrics tooadjust your pool's node count based on resource usage and task status.</span></span> <span data-ttu-id="b9713-118">다음 수식 tooconstruct를 사용 하도록 설정한 자동 풀을 모두 사용 하 여 크기를 조정 배치 REST 및.NET Api hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-118">We then describe how tooconstruct a formula and enable automatic scaling on a pool by using both hello Batch REST and .NET APIs.</span></span> <span data-ttu-id="b9713-119">마지막으로 몇 가지 예제 수식으로 마무리하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-119">Finally, we finish up with a few example formulas.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9713-120">Hello 일괄 처리 계정을 만들 때 지정할 수 있습니다 [계정 구성](batch-api-basics.md#account), 풀 일괄 처리 서비스 구독 (hello 기본값) 또는 사용자 구독에 할당 된 여부를 결정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-120">When you create a Batch account, you can specify hello [account configuration](batch-api-basics.md#account), which determines whether pools are allocated in a Batch service subscription (hello default), or in your user subscription.</span></span> <span data-ttu-id="b9713-121">Hello 기본 일괄 처리 서비스 구성을 사용 하 여 일괄 처리 계정이 만든 경우 사용자 계정은 제한 된 tooa 최대 처리를 위해 사용할 수 있는 코어 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-121">If you created your Batch account with hello default Batch Service configuration, then your account is limited tooa maximum number of cores that can be used for processing.</span></span> <span data-ttu-id="b9713-122">일괄 처리 서비스 hello toothat 코어 제한부터만 계산 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-122">hello Batch service scales compute nodes only up toothat core limit.</span></span> <span data-ttu-id="b9713-123">이러한 이유로 hello 일괄 처리 서비스 자동 크기 조정 수식에 의해 지정 된 계산 노드의 hello 대상 수에 도달 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-123">For this reason, hello Batch service may not reach hello target number of compute nodes specified by an autoscale formula.</span></span> <span data-ttu-id="b9713-124">참조 [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md) 보기 및 계정 할당량 증가에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-124">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for information on viewing and increasing your account quotas.</span></span>
>
><span data-ttu-id="b9713-125">Hello 사용자 구독 구성을 사용 하 여 계정의 만든 계정 hello 구독에 대 한 코어 할당량 hello에서에서 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-125">If you created your account with hello User Subscription configuration, then your account shares in hello core quota for hello subscription.</span></span> <span data-ttu-id="b9713-126">자세한 내용은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)에서 [Virtual Machines 제한](../azure-subscription-service-limits.md#virtual-machines-limits)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9713-126">For more information, see [Virtual Machines limits](../azure-subscription-service-limits.md#virtual-machines-limits) in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
>
>

## <a name="automatic-scaling-formulas"></a><span data-ttu-id="b9713-127">자동 크기 조정 수식</span><span class="sxs-lookup"><span data-stu-id="b9713-127">Automatic scaling formulas</span></span>
<span data-ttu-id="b9713-128">자동 크기 조정 수식은 하나 이상의 문을 포함하는 사용자가 정의한 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-128">An automatic scaling formula is a string value that you define that contains one or more statements.</span></span> <span data-ttu-id="b9713-129">hello 자동 크기 조정 수식이 tooa 풀에 할당 된 [autoScaleFormula] [ rest_autoscaleformula] 요소 (일괄 처리 REST) 또는 [CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula] 속성 (일괄 처리.NET)입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-129">hello autoscale formula is assigned tooa pool's [autoScaleFormula][rest_autoscaleformula] element (Batch REST) or [CloudPool.AutoScaleFormula][net_cloudpool_autoscaleformula] property (Batch .NET).</span></span> <span data-ttu-id="b9713-130">hello 일괄 처리 서비스는 hello 다음 처리 간격에 대 한 hello 풀의 수식 toodetermine hello 대상 수가 계산 노드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-130">hello Batch service uses your formula toodetermine hello target number of compute nodes in hello pool for hello next interval of processing.</span></span> <span data-ttu-id="b9713-131">hello 수식 문자열 8KB를 초과할 수 없습니다, 그리고 세미콜론으로 구분 되 고 줄 바꿈 및 주석을 포함할 수 있는 too100 문을를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-131">hello formula string cannot exceed 8 KB, can include up too100 statements that are separated by semicolons, and can include line breaks and comments.</span></span>

<span data-ttu-id="b9713-132">자동 크기 조정 수식은 Batch 자동 크기 조정 "언어"로 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-132">You can think of automatic scaling formulas as a Batch autoscale "language."</span></span> <span data-ttu-id="b9713-133">수식 문은 서비스 정의 변수 (hello 일괄 처리 서비스에서 정의 된 변수) 및 사용자 정의 변수 (사용자가 정의한 변수)를 모두 포함할 수 있는 자유형 식이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-133">Formula statements are free-formed expressions that can include both service-defined variables (variables defined by hello Batch service) and user-defined variables (variables that you define).</span></span> <span data-ttu-id="b9713-134">기본 제공 형식, 연산자 및 함수를 사용하여 이러한 값에 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-134">They can perform various operations on these values by using built-in types, operators, and functions.</span></span> <span data-ttu-id="b9713-135">예를 들어 문을 다음 양식 hello를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-135">For example, a statement might take hello following form:</span></span>

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

<span data-ttu-id="b9713-136">수식은 일반적으로 이전 문에서 가져온 값에 대한 작업을 수행하는 여러 문을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-136">Formulas generally contain multiple statements that perform operations on values that are obtained in previous statements.</span></span> <span data-ttu-id="b9713-137">에 대 한 값을 구한 먼저 예를 들어 `variable1`, tooa 함수 toopopulate 전달 `variable2`:</span><span class="sxs-lookup"><span data-stu-id="b9713-137">For example, first we obtain a value for `variable1`, then pass it tooa function toopopulate `variable2`:</span></span>

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

<span data-ttu-id="b9713-138">대상 수의 계산 노드 자동 크기 조정 수식 tooarrive 프로그램에서 이러한 문을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-138">Include these statements in your autoscale formula tooarrive at a target number of compute nodes.</span></span> <span data-ttu-id="b9713-139">전용 노드와 우선 순위가 낮은 노드에는 각각 자체의 목표 설정이 있으므로 각 노드 형식의 목표를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-139">Dedicated nodes and low-priority nodes each have their own target settings, so that you can define a target for each type of node.</span></span> <span data-ttu-id="b9713-140">자동 크기 조정 수식에는 전용 노드의 목표 값, 우선 순위가 낮은 노드의 목표 값 또는 둘 다가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-140">An autoscale formula can include a target value for dedicated nodes, a target value for low-priority nodes, or both.</span></span>

<span data-ttu-id="b9713-141">hello 대상 노드 수 이상에서 이하로 되었거나 hello hello 현재 hello 풀에서 해당 형식의 노드 수와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-141">hello target number of nodes may be higher, lower, or hello same as hello current number of nodes of that type in hello pool.</span></span> <span data-ttu-id="b9713-142">Batch는 풀의 자동 크기 조정 수식을 특정 간격([자동 크기 조정 간격](#automatic-scaling-interval) 참조)으로 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-142">Batch evaluates a pool's autoscale formula at a specific interval (see [automatic scaling intervals](#automatic-scaling-interval)).</span></span> <span data-ttu-id="b9713-143">각 유형의 자동 크기 조정 수식 평가 hello 시 지정 하는 hello 풀 toohello 숫자의 노드에서 hello 대상 수를 조정 하는 일괄 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-143">Batch adjusts hello target number of each type of node in hello pool toohello number that your autoscale formula specifies at hello time of evaluation.</span></span>

### <a name="sample-autoscale-formula"></a><span data-ttu-id="b9713-144">샘플 자동 크기 조정 수식</span><span class="sxs-lookup"><span data-stu-id="b9713-144">Sample autoscale formula</span></span>

<span data-ttu-id="b9713-145">대부분의 시나리오에 대 한 조정 된 toowork 일 수 있는 자동 크기 조정 수식의 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-145">Here is an example of an autoscale formula that can be adjusted toowork for most scenarios.</span></span> <span data-ttu-id="b9713-146">변수 hello `startingNumberOfVMs` 및 `maxNumberofVMs` hello 예의 수식이 조정된 tooyour 요구 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-146">hello variables `startingNumberOfVMs` and `maxNumberofVMs` in hello example formula can be adjusted tooyour needs.</span></span> <span data-ttu-id="b9713-147">이 수식은 전용된 노드를 확장 하지만 수정 된 tooapply tooscale 우선 순위가 낮은 노드도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-147">This formula scales dedicated nodes, but can be modified tooapply tooscale low-priority nodes as well.</span></span> 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

<span data-ttu-id="b9713-148">이 자동 크기 조정 수식을 사용 하 여 hello 풀은 처음에 단일 VM으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-148">With this autoscale formula, hello pool is initially created with a single VM.</span></span> <span data-ttu-id="b9713-149">hello `$PendingTasks` 메트릭을 실행 중이거나 큐에 대기 중인 작업의 hello 수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-149">hello `$PendingTasks` metric defines hello number of tasks that are running or queued.</span></span> <span data-ttu-id="b9713-150">hello 지난 180 초 동안 hello에서 보류 중인 작업의 hello 평균 수를 찾습니다 수식과 hello 설정 `$TargetDedicatedNodes` 변수 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-150">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets hello `$TargetDedicatedNodes` variable accordingly.</span></span> <span data-ttu-id="b9713-151">hello 수식은 되도록 전용 노드의 hello 대상 수 25 Vm을 초과 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-151">hello formula ensures that hello target number of dedicated nodes never exceeds 25 VMs.</span></span> <span data-ttu-id="b9713-152">새 작업 제출 되 hello 풀 자동으로 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-152">As new tasks are submitted, hello pool automatically grows.</span></span> <span data-ttu-id="b9713-153">작업 완료, Vm 하나씩 무료 되 고 hello 자동 크기 조정 수식 hello 풀을 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-153">As tasks complete, VMs become free one by one and hello autoscaling formula shrinks hello pool.</span></span>

## <a name="variables"></a><span data-ttu-id="b9713-154">variables</span><span class="sxs-lookup"><span data-stu-id="b9713-154">Variables</span></span>
<span data-ttu-id="b9713-155">자동 크기 조정 수식에는 **서비스 정의** 및 **사용자 정의** 변수를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-155">You can use both **service-defined** and **user-defined** variables in your autoscale formulas.</span></span> <span data-ttu-id="b9713-156">서비스 정의 변수 hello toohello 일괄 처리 서비스에서에서 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-156">hello service-defined variables are built in toohello Batch service.</span></span> <span data-ttu-id="b9713-157">서비스 정의 변수 일부는 읽기-쓰기이고, 일부는 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-157">Some service-defined variables are read-write, and some are read-only.</span></span> <span data-ttu-id="b9713-158">사용자 정의 변수는 사용자가 정의한 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-158">User-defined variables are variables that you define.</span></span> <span data-ttu-id="b9713-159">Hello 예의 수식을 hello 이전 섹션에 표시 된 것에서 `$TargetDedicatedNodes` 및 `$PendingTasks` 도 서비스 정의 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-159">In hello example formula shown in hello previous section, `$TargetDedicatedNodes` and `$PendingTasks` are service-defined variables.</span></span> <span data-ttu-id="b9713-160">변수 `startingNumberOfVMs` 및 `maxNumberofVMs`는 사용자 정의 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-160">Variables `startingNumberOfVMs` and `maxNumberofVMs` are user-defined variables.</span></span>

> [!NOTE]
> <span data-ttu-id="b9713-161">서비스 정의 변수에는 항상 달러($) 기호가 앞에 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-161">Service-defined variables are always preceded by a dollar sign ($).</span></span> <span data-ttu-id="b9713-162">사용자 정의 변수에 대 한 hello 달러 기호는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-162">For user-defined variables, hello dollar sign is optional.</span></span>
>
>

<span data-ttu-id="b9713-163">다음 표에서 hello 읽기 / 쓰기 권한 모두 및 읽기 전용으로 정의 된 변수 hello 일괄 처리 서비스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-163">hello following tables show both read-write and read-only variables that are defined by hello Batch service.</span></span>

<span data-ttu-id="b9713-164">있습니다 가져오고 설정할 수 있습니다 이러한 서비스 정의 변수의 hello 값 toomanage hello 계산 노드 수는 풀에서:</span><span class="sxs-lookup"><span data-stu-id="b9713-164">You can get and set hello values of these service-defined variables toomanage hello number of compute nodes in a pool:</span></span>

| <span data-ttu-id="b9713-165">읽기-쓰기 서비스 정의 변수</span><span class="sxs-lookup"><span data-stu-id="b9713-165">Read-write service-defined variables</span></span> | <span data-ttu-id="b9713-166">설명</span><span class="sxs-lookup"><span data-stu-id="b9713-166">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b9713-167">$TargetDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="b9713-167">$TargetDedicatedNodes</span></span> |<span data-ttu-id="b9713-168">hello 대상 수 전용된 hello 풀에 대 한 노드를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-168">hello target number of dedicated compute nodes for hello pool.</span></span> <span data-ttu-id="b9713-169">전용된 노드 수가 hello 풀 hello 필요한 노드 수를 항상 얻을 수 있으므로 대상으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-169">hello number of dedicated nodes is specified as a target because a pool may not always achieve hello desired number of nodes.</span></span> <span data-ttu-id="b9713-170">예를 들어 전용 노드의 hello 대상 수 수정 되 면 hello 하기 전에 자동 크기 조정 평가 하 여 풀 hello 최초 목표에 도달 다음 hello 풀 hello 목표에 도달 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-170">For example, if hello target number of dedicated nodes is modified by an autoscale evaluation before hello pool has reached hello initial target, then hello pool may not reach hello target.</span></span> <br /><br /> <span data-ttu-id="b9713-171">Hello 일괄 처리 서비스 구성을 사용 하 여 생성 된 계정에서 풀 hello 대상 일괄 처리 계정 노드나 코어 할당량을 초과 하는 경우 목표를 얻지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-171">A pool in an account created with hello Batch Service configuration may not achieve its target if hello target exceeds a Batch account node or core quota.</span></span> <span data-ttu-id="b9713-172">Hello 사용자 구독 구성으로 생성 하는 계정에 풀 hello 대상 hello 구독에 대 한 hello 공유 코어 할당량을 초과 하는 경우 목표를 얻지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-172">A pool in an account created with hello User Subscription configuration may not achieve its target if hello target exceeds hello shared core quota for hello subscription.</span></span>|
| <span data-ttu-id="b9713-173">$TargetLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="b9713-173">$TargetLowPriorityNodes</span></span> |<span data-ttu-id="b9713-174">hello 대상 수가 우선 순위가 낮은 hello 풀에 대 한 노드를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-174">hello target number of low-priority compute nodes for hello pool.</span></span> <span data-ttu-id="b9713-175">우선 순위가 낮은 노드 수가 hello 풀 hello 필요한 노드 수를 항상 얻을 수 있으므로 대상으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-175">hello number of low-priority nodes is specified as a target because a pool may not always achieve hello desired number of nodes.</span></span> <span data-ttu-id="b9713-176">예를 들어 우선 순위가 낮은 노드의 hello 대상 수 수정 되 면 hello 하기 전에 자동 크기 조정 평가 하 여 풀 hello 최초 목표에 도달 다음 hello 풀 hello 목표에 도달 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-176">For example, if hello target number of low-priority nodes is modified by an autoscale evaluation before hello pool has reached hello initial target, then hello pool may not reach hello target.</span></span> <span data-ttu-id="b9713-177">풀을 수도 얻지 못할 대상 hello 대상 일괄 처리 계정 노드나 코어 할당량을 초과 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="b9713-177">A pool may also not achieve its target if hello target exceeds a Batch account node or core quota.</span></span> <br /><br /> <span data-ttu-id="b9713-178">우선 순위가 낮은 계산 노드에 대한 자세한 내용은 [Batch(미리 보기)에서 낮은 우선 순위 VM 사용](batch-low-pri-vms.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9713-178">For more information on low-priority compute nodes, see [Use low-priority VMs with Batch (Preview)](batch-low-pri-vms.md).</span></span> |
| <span data-ttu-id="b9713-179">$NodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="b9713-179">$NodeDeallocationOption</span></span> |<span data-ttu-id="b9713-180">계산 노드는 풀에서 제거할 때 발생 하는 hello 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-180">hello action that occurs when compute nodes are removed from a pool.</span></span> <span data-ttu-id="b9713-181">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-181">Possible values are:</span></span><ul><li><span data-ttu-id="b9713-182">**다시 대기**-작업을 즉시 종료 하 고 다시 예약할 수 있도록 hello 작업 큐에 다시 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-182">**requeue**--Terminates tasks immediately and puts them back on hello job queue so that they are rescheduled.</span></span><li><span data-ttu-id="b9713-183">**종료**-작업을 즉시 종료 하 고 hello 작업 큐에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-183">**terminate**--Terminates tasks immediately and removes them from hello job queue.</span></span><li><span data-ttu-id="b9713-184">**taskcompletion**-때까지 대기 toofinish 현재 실행 중인 작업과 다음 hello 풀에서 hello 노드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-184">**taskcompletion**--Waits for currently running tasks toofinish and then removes hello node from hello pool.</span></span><li><span data-ttu-id="b9713-185">**retaineddata**-에 있는 모든 hello 로컬 태스크 보존 데이터가 hello 노드 toobe 대기 hello 노드 hello 풀에서 제거 하기 전에 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-185">**retaineddata**--Waits for all hello local task-retained data on hello node toobe cleaned up before removing hello node from hello pool.</span></span></ul> |

<span data-ttu-id="b9713-186">Hello 일괄 처리 서비스에서 메트릭을 기반으로 하는 서비스 정의 변수 toomake 조정의 hello 값을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-186">You can get hello value of these service-defined variables toomake adjustments that are based on metrics from hello Batch service:</span></span>

| <span data-ttu-id="b9713-187">읽기 전용 서비스 정의 변수</span><span class="sxs-lookup"><span data-stu-id="b9713-187">Read-only service-defined variables</span></span> | <span data-ttu-id="b9713-188">설명</span><span class="sxs-lookup"><span data-stu-id="b9713-188">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b9713-189">$CPUPercent</span><span class="sxs-lookup"><span data-stu-id="b9713-189">$CPUPercent</span></span> |<span data-ttu-id="b9713-190">hello CPU 사용량 평균 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-190">hello average percentage of CPU usage.</span></span> |
| <span data-ttu-id="b9713-191">$WallClockSeconds</span><span class="sxs-lookup"><span data-stu-id="b9713-191">$WallClockSeconds</span></span> |<span data-ttu-id="b9713-192">사용 하는 시간 (초) hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-192">hello number of seconds consumed.</span></span> |
| <span data-ttu-id="b9713-193">$MemoryBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-193">$MemoryBytes</span></span> |<span data-ttu-id="b9713-194">hello 사용 (메가바이트)의 평균 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-194">hello average number of megabytes used.</span></span> |
| <span data-ttu-id="b9713-195">$DiskBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-195">$DiskBytes</span></span> |<span data-ttu-id="b9713-196">hello hello 로컬 디스크에 사용 되는 기가바이트의 평균 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-196">hello average number of gigabytes used on hello local disks.</span></span> |
| <span data-ttu-id="b9713-197">$DiskReadBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-197">$DiskReadBytes</span></span> |<span data-ttu-id="b9713-198">hello 읽은 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-198">hello number of bytes read.</span></span> |
| <span data-ttu-id="b9713-199">$DiskWriteBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-199">$DiskWriteBytes</span></span> |<span data-ttu-id="b9713-200">hello 쓴 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-200">hello number of bytes written.</span></span> |
| <span data-ttu-id="b9713-201">$DiskReadOps</span><span class="sxs-lookup"><span data-stu-id="b9713-201">$DiskReadOps</span></span> |<span data-ttu-id="b9713-202">디스크 읽기 작업의 hello 수 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-202">hello count of read disk operations performed.</span></span> |
| <span data-ttu-id="b9713-203">$DiskWriteOps</span><span class="sxs-lookup"><span data-stu-id="b9713-203">$DiskWriteOps</span></span> |<span data-ttu-id="b9713-204">hello 디스크 쓰기 작업 수행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-204">hello count of write disk operations performed.</span></span> |
| <span data-ttu-id="b9713-205">$NetworkInBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-205">$NetworkInBytes</span></span> |<span data-ttu-id="b9713-206">hello 인바운드 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-206">hello number of inbound bytes.</span></span> |
| <span data-ttu-id="b9713-207">$NetworkOutBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-207">$NetworkOutBytes</span></span> |<span data-ttu-id="b9713-208">hello 아웃 바운드 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-208">hello number of outbound bytes.</span></span> |
| <span data-ttu-id="b9713-209">$SampleNodeCount</span><span class="sxs-lookup"><span data-stu-id="b9713-209">$SampleNodeCount</span></span> |<span data-ttu-id="b9713-210">hello 계산 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-210">hello count of compute nodes.</span></span> |
| <span data-ttu-id="b9713-211">$ActiveTasks</span><span class="sxs-lookup"><span data-stu-id="b9713-211">$ActiveTasks</span></span> |<span data-ttu-id="b9713-212">hello 수 준비 tooexecute 되어 있지만 아직 실행 되지 않는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-212">hello number of tasks that are ready tooexecute but are not yet executing.</span></span> <span data-ttu-id="b9713-213">hello $ActiveTasks 수 hello 활성 상태에 있으며 종속성 조건이 충족 되는 모든 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-213">hello $ActiveTasks count includes all tasks that are in hello active state and whose dependencies have been satisfied.</span></span> <span data-ttu-id="b9713-214">Hello 활성 상태에 있지만 종속성이 충족 되지 않은 모든 작업은 hello $ActiveTasks 개수에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-214">Any tasks that are in hello active state but whose dependencies have not been satisfied are excluded from hello $ActiveTasks count.</span></span>|
| <span data-ttu-id="b9713-215">$RunningTasks</span><span class="sxs-lookup"><span data-stu-id="b9713-215">$RunningTasks</span></span> |<span data-ttu-id="b9713-216">태스크 실행 중 상태로 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-216">hello number of tasks in a running state.</span></span> |
| <span data-ttu-id="b9713-217">$PendingTasks</span><span class="sxs-lookup"><span data-stu-id="b9713-217">$PendingTasks</span></span> |<span data-ttu-id="b9713-218">$ActiveTasks 및 $RunningTasks hello 합입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-218">hello sum of $ActiveTasks and $RunningTasks.</span></span> |
| <span data-ttu-id="b9713-219">$SucceededTasks</span><span class="sxs-lookup"><span data-stu-id="b9713-219">$SucceededTasks</span></span> |<span data-ttu-id="b9713-220">hello 성공적으로 완료 하는 작업 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-220">hello number of tasks that finished successfully.</span></span> |
| <span data-ttu-id="b9713-221">$FailedTasks</span><span class="sxs-lookup"><span data-stu-id="b9713-221">$FailedTasks</span></span> |<span data-ttu-id="b9713-222">hello 실패 한 태스크 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-222">hello number of tasks that failed.</span></span> |
| <span data-ttu-id="b9713-223">$CurrentDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="b9713-223">$CurrentDedicatedNodes</span></span> |<span data-ttu-id="b9713-224">hello 현재 개수 전용된 노드를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-224">hello current number of dedicated compute nodes.</span></span> |
| <span data-ttu-id="b9713-225">$CurrentLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="b9713-225">$CurrentLowPriorityNodes</span></span> |<span data-ttu-id="b9713-226">hello 현재 수가 우선 순위가 낮은 중지 되었던 모든 노드를 포함 하 여 노드를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-226">hello current number of low-priority compute nodes, including any nodes that have been pre-empted.</span></span> |
| <span data-ttu-id="b9713-227">$PreemptedNodeCount</span><span class="sxs-lookup"><span data-stu-id="b9713-227">$PreemptedNodeCount</span></span> | <span data-ttu-id="b9713-228">중지 상태에 있는 hello 풀에 있는 노드의 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-228">hello number of nodes in hello pool that are in a pre-empted state.</span></span> |

> [!TIP]
> <span data-ttu-id="b9713-229">hello hello 이전 표에 표시 되는 서비스 정의 읽기 전용 변수는 *개체* 다양 한 메서드를 제공 하는 각 연결 된 tooaccess 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-229">hello read-only, service-defined variables that are shown in hello previous table are *objects* that provide various methods tooaccess data associated with each.</span></span> <span data-ttu-id="b9713-230">자세한 내용은 이 문서의 뒷부분에 나오는 [샘플 데이터 가져오기](#getsampledata)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9713-230">For more information, see [Obtain sample data](#getsampledata) later in this article.</span></span>
>
>

## <a name="types"></a><span data-ttu-id="b9713-231">형식</span><span class="sxs-lookup"><span data-stu-id="b9713-231">Types</span></span>
<span data-ttu-id="b9713-232">수식에 지원되는 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-232">These types are supported in a formula:</span></span>

* <span data-ttu-id="b9713-233">double</span><span class="sxs-lookup"><span data-stu-id="b9713-233">double</span></span>
* <span data-ttu-id="b9713-234">doubleVec</span><span class="sxs-lookup"><span data-stu-id="b9713-234">doubleVec</span></span>
* <span data-ttu-id="b9713-235">doubleVecList</span><span class="sxs-lookup"><span data-stu-id="b9713-235">doubleVecList</span></span>
* <span data-ttu-id="b9713-236">string</span><span class="sxs-lookup"><span data-stu-id="b9713-236">string</span></span>
* <span data-ttu-id="b9713-237">타임 스탬프-타임 스탬프는 hello 다음 멤버를 포함 하는 복합 구조:</span><span class="sxs-lookup"><span data-stu-id="b9713-237">timestamp--timestamp is a compound structure that contains hello following members:</span></span>

  * <span data-ttu-id="b9713-238">year</span><span class="sxs-lookup"><span data-stu-id="b9713-238">year</span></span>
  * <span data-ttu-id="b9713-239">month (1-12)</span><span class="sxs-lookup"><span data-stu-id="b9713-239">month (1-12)</span></span>
  * <span data-ttu-id="b9713-240">day (1-31)</span><span class="sxs-lookup"><span data-stu-id="b9713-240">day (1-31)</span></span>
  * <span data-ttu-id="b9713-241">요일 (소수점 숫자의 hello 형식에서 예를 들어 1은 월요일)</span><span class="sxs-lookup"><span data-stu-id="b9713-241">weekday (in hello format of number; for example, 1 for Monday)</span></span>
  * <span data-ttu-id="b9713-242">hour(24시간 형식, 예: 13은 오후 1시를 의미함)</span><span class="sxs-lookup"><span data-stu-id="b9713-242">hour (in 24-hour number format; for example, 13 means 1 PM)</span></span>
  * <span data-ttu-id="b9713-243">minute (00-59)</span><span class="sxs-lookup"><span data-stu-id="b9713-243">minute (00-59)</span></span>
  * <span data-ttu-id="b9713-244">second (00-59)</span><span class="sxs-lookup"><span data-stu-id="b9713-244">second (00-59)</span></span>
* <span data-ttu-id="b9713-245">timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-245">timeinterval</span></span>

  * <span data-ttu-id="b9713-246">TimeInterval_Zero</span><span class="sxs-lookup"><span data-stu-id="b9713-246">TimeInterval_Zero</span></span>
  * <span data-ttu-id="b9713-247">TimeInterval_100ns</span><span class="sxs-lookup"><span data-stu-id="b9713-247">TimeInterval_100ns</span></span>
  * <span data-ttu-id="b9713-248">TimeInterval_Microsecond</span><span class="sxs-lookup"><span data-stu-id="b9713-248">TimeInterval_Microsecond</span></span>
  * <span data-ttu-id="b9713-249">TimeInterval_Millisecond</span><span class="sxs-lookup"><span data-stu-id="b9713-249">TimeInterval_Millisecond</span></span>
  * <span data-ttu-id="b9713-250">TimeInterval_Second</span><span class="sxs-lookup"><span data-stu-id="b9713-250">TimeInterval_Second</span></span>
  * <span data-ttu-id="b9713-251">TimeInterval_Minute</span><span class="sxs-lookup"><span data-stu-id="b9713-251">TimeInterval_Minute</span></span>
  * <span data-ttu-id="b9713-252">TimeInterval_Hour</span><span class="sxs-lookup"><span data-stu-id="b9713-252">TimeInterval_Hour</span></span>
  * <span data-ttu-id="b9713-253">TimeInterval_Day</span><span class="sxs-lookup"><span data-stu-id="b9713-253">TimeInterval_Day</span></span>
  * <span data-ttu-id="b9713-254">TimeInterval_Week</span><span class="sxs-lookup"><span data-stu-id="b9713-254">TimeInterval_Week</span></span>
  * <span data-ttu-id="b9713-255">TimeInterval_Year</span><span class="sxs-lookup"><span data-stu-id="b9713-255">TimeInterval_Year</span></span>

## <a name="operations"></a><span data-ttu-id="b9713-256">작업</span><span class="sxs-lookup"><span data-stu-id="b9713-256">Operations</span></span>
<span data-ttu-id="b9713-257">이러한 작업은 hello 이전 섹션에 나열 된 hello 형식에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-257">These operations are allowed on hello types that are listed in hello previous section.</span></span>

| <span data-ttu-id="b9713-258">작업</span><span class="sxs-lookup"><span data-stu-id="b9713-258">Operation</span></span> | <span data-ttu-id="b9713-259">지원되는 연산자</span><span class="sxs-lookup"><span data-stu-id="b9713-259">Supported operators</span></span> | <span data-ttu-id="b9713-260">결과 형식</span><span class="sxs-lookup"><span data-stu-id="b9713-260">Result type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9713-261">double *operator* double</span><span class="sxs-lookup"><span data-stu-id="b9713-261">double *operator* double</span></span> |<span data-ttu-id="b9713-262">+, -, *, /</span><span class="sxs-lookup"><span data-stu-id="b9713-262">+, -, *, /</span></span> |<span data-ttu-id="b9713-263">double</span><span class="sxs-lookup"><span data-stu-id="b9713-263">double</span></span> |
| <span data-ttu-id="b9713-264">double *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-264">double *operator* timeinterval</span></span> |* |<span data-ttu-id="b9713-265">timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-265">timeinterval</span></span> |
| <span data-ttu-id="b9713-266">doubleVec *operator* double</span><span class="sxs-lookup"><span data-stu-id="b9713-266">doubleVec *operator* double</span></span> |<span data-ttu-id="b9713-267">+, -, *, /</span><span class="sxs-lookup"><span data-stu-id="b9713-267">+, -, *, /</span></span> |<span data-ttu-id="b9713-268">doubleVec</span><span class="sxs-lookup"><span data-stu-id="b9713-268">doubleVec</span></span> |
| <span data-ttu-id="b9713-269">doubleVec *operator* doubleVec</span><span class="sxs-lookup"><span data-stu-id="b9713-269">doubleVec *operator* doubleVec</span></span> |<span data-ttu-id="b9713-270">+, -, *, /</span><span class="sxs-lookup"><span data-stu-id="b9713-270">+, -, *, /</span></span> |<span data-ttu-id="b9713-271">doubleVec</span><span class="sxs-lookup"><span data-stu-id="b9713-271">doubleVec</span></span> |
| <span data-ttu-id="b9713-272">timeinterval *operator* double</span><span class="sxs-lookup"><span data-stu-id="b9713-272">timeinterval *operator* double</span></span> |<span data-ttu-id="b9713-273">*, /</span><span class="sxs-lookup"><span data-stu-id="b9713-273">*, /</span></span> |<span data-ttu-id="b9713-274">timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-274">timeinterval</span></span> |
| <span data-ttu-id="b9713-275">timeinterval *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-275">timeinterval *operator* timeinterval</span></span> |<span data-ttu-id="b9713-276">+, -</span><span class="sxs-lookup"><span data-stu-id="b9713-276">+, -</span></span> |<span data-ttu-id="b9713-277">timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-277">timeinterval</span></span> |
| <span data-ttu-id="b9713-278">timeinterval *operator* timestamp</span><span class="sxs-lookup"><span data-stu-id="b9713-278">timeinterval *operator* timestamp</span></span> |+ |<span data-ttu-id="b9713-279">timestamp</span><span class="sxs-lookup"><span data-stu-id="b9713-279">timestamp</span></span> |
| <span data-ttu-id="b9713-280">timestamp *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-280">timestamp *operator* timeinterval</span></span> |+ |<span data-ttu-id="b9713-281">timestamp</span><span class="sxs-lookup"><span data-stu-id="b9713-281">timestamp</span></span> |
| <span data-ttu-id="b9713-282">timestamp *operator* timestamp</span><span class="sxs-lookup"><span data-stu-id="b9713-282">timestamp *operator* timestamp</span></span> |- |<span data-ttu-id="b9713-283">timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-283">timeinterval</span></span> |
| <span data-ttu-id="b9713-284">*operator*double</span><span class="sxs-lookup"><span data-stu-id="b9713-284">*operator*double</span></span> |<span data-ttu-id="b9713-285">-, !</span><span class="sxs-lookup"><span data-stu-id="b9713-285">-, !</span></span> |<span data-ttu-id="b9713-286">double</span><span class="sxs-lookup"><span data-stu-id="b9713-286">double</span></span> |
| <span data-ttu-id="b9713-287">*operator*timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-287">*operator*timeinterval</span></span> |- |<span data-ttu-id="b9713-288">timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-288">timeinterval</span></span> |
| <span data-ttu-id="b9713-289">double *operator* double</span><span class="sxs-lookup"><span data-stu-id="b9713-289">double *operator* double</span></span> |<span data-ttu-id="b9713-290"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="b9713-290"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="b9713-291">double</span><span class="sxs-lookup"><span data-stu-id="b9713-291">double</span></span> |
| <span data-ttu-id="b9713-292">string *operator* string</span><span class="sxs-lookup"><span data-stu-id="b9713-292">string *operator* string</span></span> |<span data-ttu-id="b9713-293"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="b9713-293"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="b9713-294">double</span><span class="sxs-lookup"><span data-stu-id="b9713-294">double</span></span> |
| <span data-ttu-id="b9713-295">timestamp *operator* timestamp</span><span class="sxs-lookup"><span data-stu-id="b9713-295">timestamp *operator* timestamp</span></span> |<span data-ttu-id="b9713-296"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="b9713-296"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="b9713-297">double</span><span class="sxs-lookup"><span data-stu-id="b9713-297">double</span></span> |
| <span data-ttu-id="b9713-298">timeinterval *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="b9713-298">timeinterval *operator* timeinterval</span></span> |<span data-ttu-id="b9713-299"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="b9713-299"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="b9713-300">double</span><span class="sxs-lookup"><span data-stu-id="b9713-300">double</span></span> |
| <span data-ttu-id="b9713-301">double *operator* double</span><span class="sxs-lookup"><span data-stu-id="b9713-301">double *operator* double</span></span> |<span data-ttu-id="b9713-302">&&, &#124;&#124;</span><span class="sxs-lookup"><span data-stu-id="b9713-302">&&, &#124;&#124;</span></span> |<span data-ttu-id="b9713-303">double</span><span class="sxs-lookup"><span data-stu-id="b9713-303">double</span></span> |

<span data-ttu-id="b9713-304">3항 연산자(`double ? statement1 : statement2`)가 있는 이중 연산자를 테스트할 경우 0이 아님이 **true**이고 0은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-304">When testing a double with a ternary operator (`double ? statement1 : statement2`), nonzero is **true**, and zero is **false**.</span></span>

## <a name="functions"></a><span data-ttu-id="b9713-305">함수</span><span class="sxs-lookup"><span data-stu-id="b9713-305">Functions</span></span>
<span data-ttu-id="b9713-306">이러한 미리 정의 된 **함수** toouse는 자동 크기 조정 수식을 정의 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-306">These predefined **functions** are available for you toouse in defining an automatic scaling formula.</span></span>

| <span data-ttu-id="b9713-307">함수</span><span class="sxs-lookup"><span data-stu-id="b9713-307">Function</span></span> | <span data-ttu-id="b9713-308">반환 형식</span><span class="sxs-lookup"><span data-stu-id="b9713-308">Return type</span></span> | <span data-ttu-id="b9713-309">설명</span><span class="sxs-lookup"><span data-stu-id="b9713-309">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9713-310">avg(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-310">avg(doubleVecList)</span></span> |<span data-ttu-id="b9713-311">double</span><span class="sxs-lookup"><span data-stu-id="b9713-311">double</span></span> |<span data-ttu-id="b9713-312">반환 hello hello doubleVecList의 모든 값에 대 한 평균 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-312">Returns hello average value for all values in hello doubleVecList.</span></span> |
| <span data-ttu-id="b9713-313">len(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-313">len(doubleVecList)</span></span> |<span data-ttu-id="b9713-314">double</span><span class="sxs-lookup"><span data-stu-id="b9713-314">double</span></span> |<span data-ttu-id="b9713-315">반환 hello hello doubleVecList에서 생성 되는 hello 벡터의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-315">Returns hello length of hello vector that is created from hello doubleVecList.</span></span> |
| <span data-ttu-id="b9713-316">lg(double)</span><span class="sxs-lookup"><span data-stu-id="b9713-316">lg(double)</span></span> |<span data-ttu-id="b9713-317">double</span><span class="sxs-lookup"><span data-stu-id="b9713-317">double</span></span> |<span data-ttu-id="b9713-318">반환 hello 로그 밑이 2 hello double 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-318">Returns hello log base 2 of hello double.</span></span> |
| <span data-ttu-id="b9713-319">lg(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-319">lg(doubleVecList)</span></span> |<span data-ttu-id="b9713-320">doubleVec</span><span class="sxs-lookup"><span data-stu-id="b9713-320">doubleVec</span></span> |<span data-ttu-id="b9713-321">밑이 2 hello doubleVecList hello component-wise 로그를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-321">Returns hello component-wise log base 2 of hello doubleVecList.</span></span> <span data-ttu-id="b9713-322">vec(double) hello 매개 변수에 대해 명시적으로 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-322">A vec(double) must be explicitly passed for hello parameter.</span></span> <span data-ttu-id="b9713-323">그렇지 않으면 hello double lg (double) 버전으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-323">Otherwise, hello double lg(double) version is assumed.</span></span> |
| <span data-ttu-id="b9713-324">ln(double)</span><span class="sxs-lookup"><span data-stu-id="b9713-324">ln(double)</span></span> |<span data-ttu-id="b9713-325">double</span><span class="sxs-lookup"><span data-stu-id="b9713-325">double</span></span> |<span data-ttu-id="b9713-326">반환 hello hello double의 자연 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-326">Returns hello natural log of hello double.</span></span> |
| <span data-ttu-id="b9713-327">ln(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-327">ln(doubleVecList)</span></span> |<span data-ttu-id="b9713-328">doubleVec</span><span class="sxs-lookup"><span data-stu-id="b9713-328">doubleVec</span></span> |<span data-ttu-id="b9713-329">밑이 2 hello doubleVecList hello component-wise 로그를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-329">Returns hello component-wise log base 2 of hello doubleVecList.</span></span> <span data-ttu-id="b9713-330">vec(double) hello 매개 변수에 대해 명시적으로 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-330">A vec(double) must be explicitly passed for hello parameter.</span></span> <span data-ttu-id="b9713-331">그렇지 않으면 hello double lg (double) 버전으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-331">Otherwise, hello double lg(double) version is assumed.</span></span> |
| <span data-ttu-id="b9713-332">log(double)</span><span class="sxs-lookup"><span data-stu-id="b9713-332">log(double)</span></span> |<span data-ttu-id="b9713-333">double</span><span class="sxs-lookup"><span data-stu-id="b9713-333">double</span></span> |<span data-ttu-id="b9713-334">Hello 로그 밑수 10을 반환 hello double입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-334">Returns hello log base 10 of hello double.</span></span> |
| <span data-ttu-id="b9713-335">log(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-335">log(doubleVecList)</span></span> |<span data-ttu-id="b9713-336">doubleVec</span><span class="sxs-lookup"><span data-stu-id="b9713-336">doubleVec</span></span> |<span data-ttu-id="b9713-337">Hello component-wise 로그 hello doubleVecList의 밑수 10을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-337">Returns hello component-wise log base 10 of hello doubleVecList.</span></span> <span data-ttu-id="b9713-338">vec(double) hello 단일 double 매개 변수에 대해 명시적으로 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-338">A vec(double) must be explicitly passed for hello single double parameter.</span></span> <span data-ttu-id="b9713-339">그렇지 않으면 hello log (double) 버전으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-339">Otherwise, hello double log(double) version is assumed.</span></span> |
| <span data-ttu-id="b9713-340">max(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-340">max(doubleVecList)</span></span> |<span data-ttu-id="b9713-341">double</span><span class="sxs-lookup"><span data-stu-id="b9713-341">double</span></span> |<span data-ttu-id="b9713-342">반환 hello hello doubleVecList의 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-342">Returns hello maximum value in hello doubleVecList.</span></span> |
| <span data-ttu-id="b9713-343">min(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-343">min(doubleVecList)</span></span> |<span data-ttu-id="b9713-344">double</span><span class="sxs-lookup"><span data-stu-id="b9713-344">double</span></span> |<span data-ttu-id="b9713-345">반환 hello hello doubleVecList의 최소값입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-345">Returns hello minimum value in hello doubleVecList.</span></span> |
| <span data-ttu-id="b9713-346">norm(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-346">norm(doubleVecList)</span></span> |<span data-ttu-id="b9713-347">double</span><span class="sxs-lookup"><span data-stu-id="b9713-347">double</span></span> |<span data-ttu-id="b9713-348">반환 hello hello doubleVecList에서 생성 되는 hello 벡터의 2-norm 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-348">Returns hello two-norm of hello vector that is created from hello doubleVecList.</span></span> |
| <span data-ttu-id="b9713-349">percentile(doubleVec v, double p)</span><span class="sxs-lookup"><span data-stu-id="b9713-349">percentile(doubleVec v, double p)</span></span> |<span data-ttu-id="b9713-350">double</span><span class="sxs-lookup"><span data-stu-id="b9713-350">double</span></span> |<span data-ttu-id="b9713-351">반환 hello hello 벡터 v의 백분위 수 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-351">Returns hello percentile element of hello vector v.</span></span> |
| <span data-ttu-id="b9713-352">rand()</span><span class="sxs-lookup"><span data-stu-id="b9713-352">rand()</span></span> |<span data-ttu-id="b9713-353">double</span><span class="sxs-lookup"><span data-stu-id="b9713-353">double</span></span> |<span data-ttu-id="b9713-354">0.0에서 1.0 사이의 임의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-354">Returns a random value between 0.0 and 1.0.</span></span> |
| <span data-ttu-id="b9713-355">range(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-355">range(doubleVecList)</span></span> |<span data-ttu-id="b9713-356">double</span><span class="sxs-lookup"><span data-stu-id="b9713-356">double</span></span> |<span data-ttu-id="b9713-357">Hello doubleveclist에서 hello hello 최소 및 최대 값의 차이 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-357">Returns hello difference between hello min and max values in hello doubleVecList.</span></span> |
| <span data-ttu-id="b9713-358">std(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-358">std(doubleVecList)</span></span> |<span data-ttu-id="b9713-359">double</span><span class="sxs-lookup"><span data-stu-id="b9713-359">double</span></span> |<span data-ttu-id="b9713-360">반환 hello hello doubleVecList의 hello 값 샘플 표준 편차입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-360">Returns hello sample standard deviation of hello values in hello doubleVecList.</span></span> |
| <span data-ttu-id="b9713-361">stop()</span><span class="sxs-lookup"><span data-stu-id="b9713-361">stop()</span></span> | |<span data-ttu-id="b9713-362">Hello 자동 크기 조정 식의 평가 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-362">Stops evaluation of hello autoscaling expression.</span></span> |
| <span data-ttu-id="b9713-363">sum(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="b9713-363">sum(doubleVecList)</span></span> |<span data-ttu-id="b9713-364">double</span><span class="sxs-lookup"><span data-stu-id="b9713-364">double</span></span> |<span data-ttu-id="b9713-365">반환 hello 전체적인 hello doubleVecList의 모든 hello 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-365">Returns hello sum of all hello components of hello doubleVecList.</span></span> |
| <span data-ttu-id="b9713-366">time(string dateTime="")</span><span class="sxs-lookup"><span data-stu-id="b9713-366">time(string dateTime="")</span></span> |<span data-ttu-id="b9713-367">timestamp</span><span class="sxs-lookup"><span data-stu-id="b9713-367">timestamp</span></span> |<span data-ttu-id="b9713-368">매개 변수가 전달 되는 경우 또는 전달 되 면 hello dateTime 문자열의 타임 스탬프를 환영 하는 경우 hello의 타임 스탬프 hello 현재 시간을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-368">Returns hello time stamp of hello current time if no parameters are passed, or hello time stamp of hello dateTime string if it is passed.</span></span> <span data-ttu-id="b9713-369">지원되는 dateTime 형식은 W3C-DTF 및 RFC 1123입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-369">Supported dateTime formats are W3C-DTF and RFC 1123.</span></span> |
| <span data-ttu-id="b9713-370">val(doubleVec v, double i)</span><span class="sxs-lookup"><span data-stu-id="b9713-370">val(doubleVec v, double i)</span></span> |<span data-ttu-id="b9713-371">double</span><span class="sxs-lookup"><span data-stu-id="b9713-371">double</span></span> |<span data-ttu-id="b9713-372">시작 인덱스가 0 인 벡터 v의에서 위치 i에 있는 hello 요소의 hello 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-372">Returns hello value of hello element that is at location i in vector v, with a starting index of zero.</span></span> |

<span data-ttu-id="b9713-373">목록을 수락할 hello 앞의 표에서 설명 하는 hello 함수 중 일부를 인수로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-373">Some of hello functions that are described in hello previous table can accept a list as an argument.</span></span> <span data-ttu-id="b9713-374">hello 쉼표로 구분 된 목록은 어떠한 조합의 *double* 및 *doubleVec*합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-374">hello comma-separated list is any combination of *double* and *doubleVec*.</span></span> <span data-ttu-id="b9713-375">예:</span><span class="sxs-lookup"><span data-stu-id="b9713-375">For example:</span></span>

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

<span data-ttu-id="b9713-376">hello *doubleVecList* 값은 변환 된 tooa 단일 *doubleVec* 평가 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="b9713-376">hello *doubleVecList* value is converted tooa single *doubleVec* before evaluation.</span></span> <span data-ttu-id="b9713-377">예를 들어 경우 `v = [1,2,3]`를 호출한 다음 `avg(v)` 해당 toocalling은 `avg(1,2,3)`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-377">For example, if `v = [1,2,3]`, then calling `avg(v)` is equivalent toocalling `avg(1,2,3)`.</span></span> <span data-ttu-id="b9713-378">호출 `avg(v, 7)` 해당 toocalling은 `avg(1,2,3,7)`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-378">Calling `avg(v, 7)` is equivalent toocalling `avg(1,2,3,7)`.</span></span>

## <span data-ttu-id="b9713-379"><a name="getsampledata"></a>샘플 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9713-379"><a name="getsampledata"></a>Obtain sample data</span></span>
<span data-ttu-id="b9713-380">자동 크기 조정 수식 hello 일괄 처리 서비스에서 제공 되는 메트릭 데이터 (샘플)에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-380">Autoscale formulas act on metrics data (samples) that is provided by hello Batch service.</span></span> <span data-ttu-id="b9713-381">수식을 확장 하거나 hello 서비스에서 얻은 hello 값에 따라 풀 크기를 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-381">A formula grows or shrinks pool size based on hello values that it obtains from hello service.</span></span> <span data-ttu-id="b9713-382">설명한 hello 서비스 정의 된 변수는 이전에 tooaccess 데이터를 해당 개체와 연결 된 다양 한 메서드를 제공 하는 개체는입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-382">hello service-defined variables that were described previously are objects that provide various methods tooaccess data that is associated with that object.</span></span> <span data-ttu-id="b9713-383">예를 들어 hello 다음 식을 보여 줍니다 요청 tooget hello 지난 5 분 동안 CPU 사용량:</span><span class="sxs-lookup"><span data-stu-id="b9713-383">For example, hello following expression shows a request tooget hello last five minutes of CPU usage:</span></span>

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| <span data-ttu-id="b9713-384">메서드</span><span class="sxs-lookup"><span data-stu-id="b9713-384">Method</span></span> | <span data-ttu-id="b9713-385">설명</span><span class="sxs-lookup"><span data-stu-id="b9713-385">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b9713-386">GetSample()</span><span class="sxs-lookup"><span data-stu-id="b9713-386">GetSample()</span></span> |<span data-ttu-id="b9713-387">hello `GetSample()` 메서드 데이터 샘플의 벡터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-387">hello `GetSample()` method returns a vector of data samples.</span></span><br/><br/><span data-ttu-id="b9713-388">하나의 샘플은 30초 동안의 메트릭 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-388">A sample is 30 seconds worth of metrics data.</span></span> <span data-ttu-id="b9713-389">즉 30초마다 샘플을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-389">In other words, samples are obtained every 30 seconds.</span></span> <span data-ttu-id="b9713-390">하지만 아래 설명과 같이 샘플 수집 하는 경우와 사용 가능한 tooa 수식을 때 까지는 지연 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-390">But as noted below, there is a delay between when a sample is collected and when it is available tooa formula.</span></span> <span data-ttu-id="b9713-391">따라서 지정된 기간 동안 일부 샘플을 수식에 의한 평가에 사용할 수 없을지도 모릅니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-391">As such, not all samples for a given time period may be available for evaluation by a formula.</span></span><ul><li>`doubleVec GetSample(double count)`<br/><span data-ttu-id="b9713-392">수집 된 가장 최근 샘플 hello에서에서 샘플 tooobtain hello 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-392">Specifies hello number of samples tooobtain from hello most recent samples that were collected.</span></span><br/><br/><span data-ttu-id="b9713-393">`GetSample(1)`hello 마지막 사용 가능한 샘플을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-393">`GetSample(1)` returns hello last available sample.</span></span> <span data-ttu-id="b9713-394">그러나 메트릭과 같이 `$CPUPercent`,이 쓰일 수 없습니다 불가능 한 tooknow 있기 때문에 *때* hello 샘플이 수집 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-394">For metrics like `$CPUPercent`, however, this should not be used because it is impossible tooknow *when* hello sample was collected.</span></span> <span data-ttu-id="b9713-395">최근 샘플일 수도 있지만 시스템 문제로 인해 훨씬 오래된 샘플일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-395">It might be recent, or, because of system issues, it might be much older.</span></span> <span data-ttu-id="b9713-396">이러한 경우 toouse 아래와 같이 시간 간격에에서 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-396">It is better in such cases toouse a time interval as shown below.</span></span><li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/><span data-ttu-id="b9713-397">샘플 데이터를 수집하기 위한 시간 프레임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-397">Specifies a time frame for gathering sample data.</span></span> <span data-ttu-id="b9713-398">필요에 따라 지정 hello에서 사용할 수 있어야 하는 샘플의 hello 백분율 시간 프레임을 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-398">Optionally, it also specifies hello percentage of samples that must be available in hello requested time frame.</span></span><br/><br/><span data-ttu-id="b9713-399">`$CPUPercent.GetSample(TimeInterval_Minute * 10)`지난 10 분 hello에 대 한 모든 샘플 hello CPUPercent 기록에 있는 경우에 20 샘플을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-399">`$CPUPercent.GetSample(TimeInterval_Minute * 10)` would return 20 samples if all samples for hello last 10 minutes are present in hello CPUPercent history.</span></span> <span data-ttu-id="b9713-400">그러나 Hello 지난 1 분간 기록 하지 않았으면만 18 샘플 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-400">If hello last minute of history was not available, however, only 18 samples would be returned.</span></span> <span data-ttu-id="b9713-401">이 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-401">In this case:</span></span><br/><br/><span data-ttu-id="b9713-402">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`hello 샘플의 90%에만 사용할 수 있으므로 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-402">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)` would fail because only 90 percent of hello samples are available.</span></span><br/><br/><span data-ttu-id="b9713-403">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)`은 성공합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-403">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` would succeed.</span></span><li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/><span data-ttu-id="b9713-404">시작 시간과 종료 시간을 사용하여 데이터를 수집하기 위한 시간 프레임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-404">Specifies a time frame for gathering data, with both a start time and an end time.</span></span><br/><br/><span data-ttu-id="b9713-405">위에서 설명 했 듯이 샘플 수집 하는 경우와 사용 가능한 tooa 수식을 때 까지는 지연 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-405">As mentioned above, there is a delay between when a sample is collected and when it is available tooa formula.</span></span> <span data-ttu-id="b9713-406">Hello를 사용 하는 경우 이러한 지연 시간을 고려 `GetSample` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b9713-406">Consider this delay when you use hello `GetSample` method.</span></span> <span data-ttu-id="b9713-407">아래 `GetSamplePercent` 참조</span><span class="sxs-lookup"><span data-stu-id="b9713-407">See `GetSamplePercent` below.</span></span> |
| <span data-ttu-id="b9713-408">GetSamplePeriod()</span><span class="sxs-lookup"><span data-stu-id="b9713-408">GetSamplePeriod()</span></span> |<span data-ttu-id="b9713-409">기록 샘플 데이터 집합에서 수행 된 샘플의 hello 기간을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-409">Returns hello period of samples that were taken in a historical sample data set.</span></span> |
| <span data-ttu-id="b9713-410">Count()</span><span class="sxs-lookup"><span data-stu-id="b9713-410">Count()</span></span> |<span data-ttu-id="b9713-411">반환 hello 총 hello 메트릭 기록에는 샘플 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-411">Returns hello total number of samples in hello metric history.</span></span> |
| <span data-ttu-id="b9713-412">HistoryBeginTime()</span><span class="sxs-lookup"><span data-stu-id="b9713-412">HistoryBeginTime()</span></span> |<span data-ttu-id="b9713-413">반환 hello hello hello 메트릭에 대 한 가장 오래 된 사용 가능한 데이터 샘플의 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-413">Returns hello time stamp of hello oldest available data sample for hello metric.</span></span> |
| <span data-ttu-id="b9713-414">GetSamplePercent()</span><span class="sxs-lookup"><span data-stu-id="b9713-414">GetSamplePercent()</span></span> |<span data-ttu-id="b9713-415">반환 hello는 주어진된 시간 간격에 사용할 수 있는 샘플의 백분율입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-415">Returns hello percentage of samples that are available for a given time interval.</span></span> <span data-ttu-id="b9713-416">예:</span><span class="sxs-lookup"><span data-stu-id="b9713-416">For example:</span></span><br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/><span data-ttu-id="b9713-417">때문에 hello `GetSample` 메서드가 반환 하는 샘플의 hello 백분율 미만이 면 hello 실패 `samplePercent` 지정 hello를 사용할 수 `GetSamplePercent` 메서드 toocheck 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-417">Because hello `GetSample` method fails if hello percentage of samples returned is less than hello `samplePercent` specified, you can use hello `GetSamplePercent` method toocheck first.</span></span> <span data-ttu-id="b9713-418">그런 다음 부족 하 여 샘플 hello 자동 크기 조정 평가 중지 하지 않고 표시 되어 있는 경우 다른 동작을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-418">Then you can perform an alternate action if insufficient samples are present, without halting hello automatic scaling evaluation.</span></span> |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a><span data-ttu-id="b9713-419">샘플, 샘플 비율 및 hello *GetSample()* 메서드</span><span class="sxs-lookup"><span data-stu-id="b9713-419">Samples, sample percentage, and hello *GetSample()* method</span></span>
<span data-ttu-id="b9713-420">자동 크기 조정 수식이의 핵심 작업 hello tooobtain 작업 및 자원 메트릭 데이터 이며 해당 데이터에 따라 풀 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-420">hello core operation of an autoscale formula is tooobtain task and resource metric data and then adjust pool size based on that data.</span></span> <span data-ttu-id="b9713-421">따라서 것은 중요 한 toohave 자동 크기 조정 수식 메트릭 데이터 (샘플)와 상호 작용 하는 방법을 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-421">As such, it is important toohave a clear understanding of how autoscale formulas interact with metrics data (samples).</span></span>

<span data-ttu-id="b9713-422">**샘플**</span><span class="sxs-lookup"><span data-stu-id="b9713-422">**Samples**</span></span>

<span data-ttu-id="b9713-423">hello 일괄 처리 서비스는 정기적으로 작업 및 자원 메트릭 샘플을 사용 하 고 자동 크기 조정 수식을 사용할 수 있는 tooyour 끌고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-423">hello Batch service periodically takes samples of task and resource metrics and makes them available tooyour autoscale formulas.</span></span> <span data-ttu-id="b9713-424">이러한 예제는 hello 일괄 처리 서비스에서 30 초 마다 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-424">These samples are recorded every 30 seconds by hello Batch service.</span></span> <span data-ttu-id="b9713-425">그러나는 일반적으로 이러한 샘플 기록 된 시간 사이의 너무 사용할 수 있습니다 (고 때에서 읽을 수)는 지연을 자동 크기 조정 수식입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-425">However, there is typically a delay between when those samples were recorded and when they are made available too(and can be read by) your autoscale formulas.</span></span> <span data-ttu-id="b9713-426">또한 네트워크나 기타 인프라 문제 toovarious 요인 인해 샘플 하지 기록 될 수 있습니다는 특정 기간에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-426">Additionally, due toovarious factors such as network or other infrastructure issues, samples may not be recorded for a particular interval.</span></span>

<span data-ttu-id="b9713-427">**샘플 비율**</span><span class="sxs-lookup"><span data-stu-id="b9713-427">**Sample percentage**</span></span>

<span data-ttu-id="b9713-428">때 `samplePercent` toohello 전달 되 `GetSample()` 메서드 또는 hello `GetSamplePercent()` 메서드는 _%_ tooa 비교 hello 가능한 최대 수 hello 일괄 처리 서비스에서 기록 되는 샘플을 참조 하 고 사용 가능한 tooyour 자동 크기 조정 수식이 있는 샘플 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-428">When `samplePercent` is passed toohello `GetSample()` method or hello `GetSamplePercent()` method is called, _percent_ refers tooa comparison between hello total possible number of samples that are recorded by hello Batch service and hello number of samples that are available tooyour autoscale formula.</span></span>

<span data-ttu-id="b9713-429">예를 들어 10분 TimeSpan을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-429">Let's look at a 10-minute timespan as an example.</span></span> <span data-ttu-id="b9713-430">샘플에는 10 분 시간 범위 내에서 30 초 마다 기록 되므로, 일괄 처리에 의해 기록 되는 샘플의 hello 최대 총 수는 20 샘플 (2 분 당) 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-430">Because samples are recorded every 30 seconds within a 10-minute timespan, hello maximum total number of samples that are recorded by Batch would be 20 samples (2 per minute).</span></span> <span data-ttu-id="b9713-431">그러나 메커니즘 및 Azure 내에서 기타 문제를 보고 하는 hello의 내재 된 대기 시간 toohello 인해 있을 수 있습니다만 15 샘플 읽기에 대 한 사용 가능한 tooyour 자동 크기 조정 수식에는.</span><span class="sxs-lookup"><span data-stu-id="b9713-431">However, due toohello inherent latency of hello reporting mechanism and other issues within Azure, there may be only 15 samples that are available tooyour autoscale formula for reading.</span></span> <span data-ttu-id="b9713-432">따라서 예를 들어 그 10 분 동안 hello 총 기록 하는 샘플 수의 75%에만 수 있습니다 사용할 수 있는 tooyour 수식입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-432">So, for example, for that 10-minute period, only 75% of hello total number of samples recorded may be available tooyour formula.</span></span>

<span data-ttu-id="b9713-433">**GetSample() 및 샘플 범위**</span><span class="sxs-lookup"><span data-stu-id="b9713-433">**GetSample() and sample ranges**</span></span>

<span data-ttu-id="b9713-434">자동 크기 조정 수식은 진행 중인 toobe 증가 및 축소 풀 &mdash; 노드 노드 추가 또는 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-434">Your autoscale formulas are going toobe growing and shrinking your pools &mdash; adding nodes or removing nodes.</span></span> <span data-ttu-id="b9713-435">노드 비용이 있습니다, 때문 분석 충분 한 데이터를 기반으로 하는 지능형 메서드를 사용 하는 수식을 tooensure를 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-435">Because nodes cost you money, you want tooensure that your formulas use an intelligent method of analysis that is based on sufficient data.</span></span> <span data-ttu-id="b9713-436">따라서 수식에서 추세 형식 분석을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-436">Therefore, we recommend that you use a trending-type analysis in your formulas.</span></span> <span data-ttu-id="b9713-437">이 형식은 수집된 샘플의 범위에 따라 풀을 확장하고 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-437">This type grows and shrinks your pools based on a range of collected samples.</span></span>

<span data-ttu-id="b9713-438">toodo를 사용 하 여 `GetSample(interval look-back start, interval look-back end)` tooreturn 벡터의 샘플:</span><span class="sxs-lookup"><span data-stu-id="b9713-438">toodo so, use `GetSample(interval look-back start, interval look-back end)` tooreturn a vector of samples:</span></span>

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

<span data-ttu-id="b9713-439">일괄 처리에 의해 줄 위에 hello 계산할 때 값의 벡터 샘플의 범위를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-439">When hello above line is evaluated by Batch, it returns a range of samples as a vector of values.</span></span> <span data-ttu-id="b9713-440">예:</span><span class="sxs-lookup"><span data-stu-id="b9713-440">For example:</span></span>

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

<span data-ttu-id="b9713-441">와 같은 함수를 유도할 수 있습니다 hello 벡터의 샘플을 수집 했습니다 면 `min()`, `max()`, 및 `avg()` tooderive hello에서 의미 있는 값 범위를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-441">Once you've collected hello vector of samples, you can then use functions like `min()`, `max()`, and `avg()` tooderive meaningful values from hello collected range.</span></span>

<span data-ttu-id="b9713-442">추가 보안을 위해 특정 기간 동안 사용할 수 있는 특정 샘플 비율 보다 작은 경우 수식 평가 toofail를 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-442">For additional security, you can force a formula evaluation toofail if less than a certain sample percentage is available for a particular time period.</span></span> <span data-ttu-id="b9713-443">수식 평가 toofail 강제 때 지시할 있습니다 일괄 처리 toocease 추가 hello 식의 평가 hello 지정 샘플의 백분율을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-443">When you force a formula evaluation toofail, you instruct Batch toocease further evaluation of hello formula if hello specified percentage of samples is not available.</span></span> <span data-ttu-id="b9713-444">이 경우에 변경 되지 않습니다 toohello 풀 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-444">In this case, no change is made toohello pool size.</span></span> <span data-ttu-id="b9713-445">hello 평가 toosucceed에 대 한 샘플의 필요한 백분율 toospecify가 세 번째 매개 변수를 너무 hello 대로 지정`GetSample()`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-445">toospecify a required percentage of samples for hello evaluation toosucceed, specify it as hello third parameter too`GetSample()`.</span></span> <span data-ttu-id="b9713-446">여기에서는 샘플의 75% 요구 사항이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-446">Here, a requirement of 75 percent of samples is specified:</span></span>

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

<span data-ttu-id="b9713-447">샘플 가용성에 지연이 있을 수 있습니다, 때문에 반드시 tooalways 모양을 다시 시작 시간이 1 분 보다 오래 된 시간 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-447">Because there may be a delay in sample availability, it is important tooalways specify a time range with a look-back start time that is older than one minute.</span></span> <span data-ttu-id="b9713-448">Hello 시스템을 통해 샘플 toopropagate hello 범위 내에 있으므로 샘플에 대 한 약 1 분 걸리는 `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-448">It takes approximately one minute for samples toopropagate through hello system, so samples in hello range `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` may not be available.</span></span> <span data-ttu-id="b9713-449">hello 백분율 매개 변수를 사용할 수는 다시 `GetSample()` tooforce 특정 샘플 비율 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-449">Again, you can use hello percentage parameter of `GetSample()` tooforce a particular sample percentage requirement.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9713-450">**자동 크기 조정 수식의 `GetSample(1)`*만* 신뢰하지 않는** 것이 **좋습니다**.</span><span class="sxs-lookup"><span data-stu-id="b9713-450">We **strongly recommend** that you **avoid relying *only* on `GetSample(1)` in your autoscale formulas**.</span></span> <span data-ttu-id="b9713-451">때문에 이것이 `GetSample(1)` toohello 일괄 처리 서비스를 "me hello를 마지막 예제 제공에 관계 없이 검색 경과한 시간입니다." 라는 내용을</span><span class="sxs-lookup"><span data-stu-id="b9713-451">This is because `GetSample(1)` essentially says toohello Batch service, "Give me hello last sample you have, no matter how long ago you retrieved it."</span></span> <span data-ttu-id="b9713-452">않을 이전 샘플 수도 가구의 단일 샘플만는 최근 작업 또는 리소스 상태 hello 더 큰 그림을 대표 하지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-452">Since it is only a single sample, and it may be an older sample, it may not be representative of hello larger picture of recent task or resource state.</span></span> <span data-ttu-id="b9713-453">사용 않으면 `GetSample(1)`, 더 큰 문의 일부 인지 확인 및 수식에 사용 하는 데이터 요소만 하지 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-453">If you do use `GetSample(1)`, make sure that it's part of a larger statement and not hello only data point that your formula relies on.</span></span>
>
>

## <a name="metrics"></a><span data-ttu-id="b9713-454">메트릭</span><span class="sxs-lookup"><span data-stu-id="b9713-454">Metrics</span></span>
<span data-ttu-id="b9713-455">수식을 정의할 때 리소스 및 작업 메트릭을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-455">You can use both resource and task metrics when you're defining a formula.</span></span> <span data-ttu-id="b9713-456">평가 하는 hello 메트릭 데이터를 기반으로 하는 hello 풀의 전용된 노드 hello 대상 수를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-456">You adjust hello target number of dedicated nodes in hello pool based on hello metrics data that you obtain and evaluate.</span></span> <span data-ttu-id="b9713-457">Hello 참조 [변수](#variables) 각 메트릭에 대 한 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="b9713-457">See hello [Variables](#variables) section above for more information on each metric.</span></span>

<table>
  <tr>
    <th><span data-ttu-id="b9713-458">메트릭</span><span class="sxs-lookup"><span data-stu-id="b9713-458">Metric</span></span></th>
    <th><span data-ttu-id="b9713-459">설명</span><span class="sxs-lookup"><span data-stu-id="b9713-459">Description</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="b9713-460"><b>리소스</b></span><span class="sxs-lookup"><span data-stu-id="b9713-460"><b>Resource</b></span></span></td>
    <td><p><span data-ttu-id="b9713-461">리소스 메트릭 hello CPU, hello 대역폭, 계산 노드의 hello 메모리 사용량을 기반으로 및 hello 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-461">Resource metrics are based on hello CPU, hello bandwidth, hello memory usage of compute nodes, and hello number of nodes.</span></span></p>
        <p> <span data-ttu-id="b9713-462">이러한 서비스 정의 변수는 노드 수에 기반하여 조정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-462">These service-defined variables are useful for making adjustments based on node count:</span></span></p>
    <p><ul>
            <li><span data-ttu-id="b9713-463">$TargetDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="b9713-463">$TargetDedicatedNodes</span></span></li>
            <li><span data-ttu-id="b9713-464">$TargetLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="b9713-464">$TargetLowPriorityNodes</span></span></li>
            <li><span data-ttu-id="b9713-465">$CurrentDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="b9713-465">$CurrentDedicatedNodes</span></span></li>
            <li><span data-ttu-id="b9713-466">$CurrentLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="b9713-466">$CurrentLowPriorityNodes</span></span></li>
            <li><span data-ttu-id="b9713-467">$preemptedNodeCount</span><span class="sxs-lookup"><span data-stu-id="b9713-467">$preemptedNodeCount</span></span></li>
            <li><span data-ttu-id="b9713-468">$SampleNodeCount</span><span class="sxs-lookup"><span data-stu-id="b9713-468">$SampleNodeCount</span></span></li>
    </ul></p>
    <p><span data-ttu-id="b9713-469">이러한 서비스 정의 변수는 노드 리소스 사용량에 기반하여 조정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-469">These service-defined variables are useful for making adjustments based on node resource usage:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="b9713-470">$CPUPercent</span><span class="sxs-lookup"><span data-stu-id="b9713-470">$CPUPercent</span></span></li>
      <li><span data-ttu-id="b9713-471">$WallClockSeconds</span><span class="sxs-lookup"><span data-stu-id="b9713-471">$WallClockSeconds</span></span></li>
      <li><span data-ttu-id="b9713-472">$MemoryBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-472">$MemoryBytes</span></span></li>
      <li><span data-ttu-id="b9713-473">$DiskBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-473">$DiskBytes</span></span></li>
      <li><span data-ttu-id="b9713-474">$DiskReadBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-474">$DiskReadBytes</span></span></li>
      <li><span data-ttu-id="b9713-475">$DiskWriteBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-475">$DiskWriteBytes</span></span></li>
      <li><span data-ttu-id="b9713-476">$DiskReadOps</span><span class="sxs-lookup"><span data-stu-id="b9713-476">$DiskReadOps</span></span></li>
      <li><span data-ttu-id="b9713-477">$DiskWriteOps</span><span class="sxs-lookup"><span data-stu-id="b9713-477">$DiskWriteOps</span></span></li>
      <li><span data-ttu-id="b9713-478">$NetworkInBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-478">$NetworkInBytes</span></span></li>
      <li><span data-ttu-id="b9713-479">$NetworkOutBytes</span><span class="sxs-lookup"><span data-stu-id="b9713-479">$NetworkOutBytes</span></span></li></ul></p>
  </tr>
  <tr>
    <td><span data-ttu-id="b9713-480"><b>Task</b></span><span class="sxs-lookup"><span data-stu-id="b9713-480"><b>Task</b></span></span></td>
    <td><p><span data-ttu-id="b9713-481">작업은 보류 중, 활성, 같은 작업의 hello 상태에 따라 메트릭과 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-481">Task metrics are based on hello status of tasks, such as Active, Pending, and Completed.</span></span> <span data-ttu-id="b9713-482">hello 다음 서비스 정의 된 변수는 작업 기준에 따라 풀 크기를 조정 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-482">hello following service-defined variables are useful for making pool-size adjustments based on task metrics:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="b9713-483">$ActiveTasks</span><span class="sxs-lookup"><span data-stu-id="b9713-483">$ActiveTasks</span></span></li>
      <li><span data-ttu-id="b9713-484">$RunningTasks</span><span class="sxs-lookup"><span data-stu-id="b9713-484">$RunningTasks</span></span></li>
      <li><span data-ttu-id="b9713-485">$PendingTasks</span><span class="sxs-lookup"><span data-stu-id="b9713-485">$PendingTasks</span></span></li>
      <li><span data-ttu-id="b9713-486">$SucceededTasks</span><span class="sxs-lookup"><span data-stu-id="b9713-486">$SucceededTasks</span></span></li>
            <li><span data-ttu-id="b9713-487">$FailedTasks</span><span class="sxs-lookup"><span data-stu-id="b9713-487">$FailedTasks</span></span></li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a><span data-ttu-id="b9713-488">자동 크기 조정 수식 작성</span><span class="sxs-lookup"><span data-stu-id="b9713-488">Write an autoscale formula</span></span>
<span data-ttu-id="b9713-489">구성 요소를 위에서 hello를 사용 하는 문을 형성 하 여 자동 크기 조정 수식을 작성 한 다음 해당 문을 완전 한 수식으로 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-489">You build an autoscale formula by forming statements that use hello above components, then combine those statements into a complete formula.</span></span> <span data-ttu-id="b9713-490">이 섹션에서는 몇 가지 실제 크기 조정을 결정할 수 있는 자동 크기 조정 수식 예제를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-490">In this section, we create an example autoscale formula that can perform some real-world scaling decisions.</span></span>

<span data-ttu-id="b9713-491">첫째, 이제 새 자동 크기 조정 수식의 hello 요구 사항을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-491">First, let's define hello requirements for our new autoscale formula.</span></span> <span data-ttu-id="b9713-492">hello 수식 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-492">hello formula should:</span></span>

1. <span data-ttu-id="b9713-493">CPU 사용량이 높은 경우 풀의 전용된 계산 노드 hello 대상 수를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-493">Increase hello target number of dedicated compute nodes in a pool if CPU usage is high.</span></span>
2. <span data-ttu-id="b9713-494">CPU 사용량이 낮을 때 풀의 전용된 계산 노드 hello 대상 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-494">Decrease hello target number of dedicated compute nodes in a pool when CPU usage is low.</span></span>
3. <span data-ttu-id="b9713-495">항상 전용된 노드 too400 hello 최대 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-495">Always restrict hello maximum number of dedicated nodes too400.</span></span>

<span data-ttu-id="b9713-496">사용자 정의 변수를 채우는 hello 보고서를 정의 하는 동안 CPU 사용량이 노드의 tooincrease hello 수 (`$totalDedicatedNodes`) 경우에만 전용 노드의 hello 현재 대상 수의 110% 있는 값을 가진 hello 최소 평균 CPU 사용량 hello 중 지난 10 분 70% 이상 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-496">tooincrease hello number of nodes during high CPU usage, define hello statement that populates a user-defined variable (`$totalDedicatedNodes`) with a value that is 110 percent of hello current target number of dedicated nodes, but only if hello minimum average CPU usage during hello last 10 minutes was above 70 percent.</span></span> <span data-ttu-id="b9713-497">그렇지 않으면 hello 현재 전용된 노드 수에 대 한 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-497">Otherwise, use hello value for hello current number of dedicated nodes.</span></span>

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

<span data-ttu-id="b9713-498">너무*감소* 중 CPU 사용량이 낮은 전용된 노드 수가 hello, 우리의 수식 집합 hello의 다음 문으로 동일 hello `$totalDedicatedNodes` 변수 too90% 경우 hello 전용 노드의 hello 현재 대상 수의 평균 CPU 사용량 hello에 지난 60 분에서 20% 였습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-498">too*decrease* hello number of dedicated nodes during low CPU usage, hello next statement in our formula sets hello same `$totalDedicatedNodes` variable too90 percent of hello current target number of dedicated nodes if hello average CPU usage in hello past 60 minutes was under 20 percent.</span></span> <span data-ttu-id="b9713-499">그렇지 않으면 hello의 현재 값을 사용 하 여 `$totalDedicatedNodes` 위의 hello 문에서 채운 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-499">Otherwise, use hello current value of `$totalDedicatedNodes` that we populated in hello statement above.</span></span>

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

<span data-ttu-id="b9713-500">이제 hello 400 전용된 계산 노드 tooa 최대 대상 수 제한:</span><span class="sxs-lookup"><span data-stu-id="b9713-500">Now limit hello target number of dedicated compute nodes tooa maximum of 400:</span></span>

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

<span data-ttu-id="b9713-501">Hello 완전 한 수식을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-501">Here's hello complete formula:</span></span>

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a><span data-ttu-id="b9713-502">.NET으로 자동 크기 조정 가능한 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="b9713-502">Create an autoscale-enabled pool with .NET</span></span>

<span data-ttu-id="b9713-503">.net을 사용 하도록 설정 하는 자동 크기 조정 기능을 사용 하 여 풀 toocreate 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="b9713-503">toocreate a pool with autoscaling enabled in .NET, follow these steps:</span></span>

1. <span data-ttu-id="b9713-504">사용 하 여 hello 풀 만들기 [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-504">Create hello pool with [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).</span></span>
2. <span data-ttu-id="b9713-505">집합 hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) 속성 너무`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-505">Set hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) property too`true`.</span></span>
3. <span data-ttu-id="b9713-506">집합 hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) 자동 크기 조정 수식 사용 하 여 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-506">Set hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) property with your autoscale formula.</span></span>
4. <span data-ttu-id="b9713-507">(선택 사항) 집합 hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) 속성 (기본값은 15 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-507">(Optional) Set hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) property (default is 15 minutes).</span></span>
5. <span data-ttu-id="b9713-508">사용 하 여 hello 풀 커밋 [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) 또는 [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-508">Commit hello pool with [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) or [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).</span></span>

<span data-ttu-id="b9713-509">hello 다음 코드 조각에서는 자동 크기 조정 가능한 풀.net에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-509">hello following code snippet creates an autoscale-enabled pool in .NET.</span></span> <span data-ttu-id="b9713-510">hello 풀의 자동 크기 조정 수식이 hello 대상의 수를 설정 월요일, 전용된 노드 too5 및 hello 주 중 일 마다 1입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-510">hello pool's autoscale formula sets hello target number of dedicated nodes too5 on Mondays, and 1 on every other day of hello week.</span></span> <span data-ttu-id="b9713-511">hello [자동 크기 조정 간격](#automatic-scaling-interval) 는 too30 시간 (분)을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-511">hello [automatic scaling interval](#automatic-scaling-interval) is set too30 minutes.</span></span> <span data-ttu-id="b9713-512">이 다른 C# 코드 조각이 문서에서는 hello 및 `myBatchClient` hello는 올바르게 초기화 된 인스턴스가 [BatchClient] [ net_batchclient] 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-512">In this and hello other C# snippets in this article, `myBatchClient` is a properly initialized instance of hello [BatchClient][net_batchclient] class.</span></span>

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="b9713-513">자동 크기 조정 가능한 풀을 만들 때 hello를 지정 하지 않으면 _targetDedicatedComputeNodes_ 매개 변수 또는 hello _targetLowPriorityComputeNodes_ hello에 매개 변수가 너무 호출 **CreatePool**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-513">When you create an autoscale-enabled pool, do not specify hello _targetDedicatedComputeNodes_ parameter or hello _targetLowPriorityComputeNodes_ parameter on hello call too**CreatePool**.</span></span> <span data-ttu-id="b9713-514">대신, hello 지정 **AutoScaleEnabled** 및 **AutoScaleFormula** hello 풀의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-514">Instead, specify hello **AutoScaleEnabled** and **AutoScaleFormula** properties on hello pool.</span></span> <span data-ttu-id="b9713-515">이러한 속성에 대 한 hello 값 각 유형의 노드에 hello 대상 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-515">hello values for these properties determine hello target number of each type of node.</span></span> <span data-ttu-id="b9713-516">Toomanually 자동 크기 조정 가능한 풀의 크기를 조정 또한 (예: [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), 첫 번째 **사용 하지 않도록 설정** 에 자동 크기 조정 풀 hello 다음 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-516">Also, toomanually resize an autoscale-enabled pool (for example, with [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), first **disable** automatic scaling on hello pool, then resize it.</span></span>
>
>

<span data-ttu-id="b9713-517">또한 tooBatch.NET을 사용할 수 있습니다 다른 hello의 [일괄 처리 Sdk](batch-apis-tools.md#azure-accounts-for-batch-development), [배치 REST](https://docs.microsoft.com/rest/api/batchservice/), [일괄 처리 PowerShell cmdlet](batch-powershell-cmdlets-get-started.md), 및 hello [일괄 처리 CLI](batch-cli-get-started.md)tooconfigure 자동 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-517">In addition tooBatch .NET, you can use any of hello other [Batch SDKs](batch-apis-tools.md#azure-accounts-for-batch-development), [Batch REST](https://docs.microsoft.com/rest/api/batchservice/), [Batch PowerShell cmdlets](batch-powershell-cmdlets-get-started.md), and hello [Batch CLI](batch-cli-get-started.md) tooconfigure autoscaling.</span></span>


### <a name="automatic-scaling-interval"></a><span data-ttu-id="b9713-518">자동 크기 조정 간격</span><span class="sxs-lookup"><span data-stu-id="b9713-518">Automatic scaling interval</span></span>
<span data-ttu-id="b9713-519">기본적으로 hello 일괄 처리 서비스가 풀의 크기에 따라 tooits 자동 크기 조정 수식이 15 분 마다 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-519">By default, hello Batch service adjusts a pool's size according tooits autoscale formula every 15 minutes.</span></span> <span data-ttu-id="b9713-520">이 간격은 다음과 같은 풀 속성 hello를 사용 하 여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-520">This interval is configurable by using hello following pool properties:</span></span>

* <span data-ttu-id="b9713-521">[CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)</span><span class="sxs-lookup"><span data-stu-id="b9713-521">[CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)</span></span>
* <span data-ttu-id="b9713-522">[autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)</span><span class="sxs-lookup"><span data-stu-id="b9713-522">[autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)</span></span>

<span data-ttu-id="b9713-523">hello 최소 간격은 5 분 이며 최대 hello 168 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-523">hello minimum interval is five minutes, and hello maximum is 168 hours.</span></span> <span data-ttu-id="b9713-524">이 범위를 벗어나는 간격을 지정 하는 경우 hello 일괄 처리 서비스는 잘못 된 요청 (400) 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-524">If an interval outside this range is specified, hello Batch service returns a Bad Request (400) error.</span></span>

> [!NOTE]
> <span data-ttu-id="b9713-525">자동 크기 조정에 1 분 미만, 현재 상태의 toorespond toochanges은 아니지만 보다는 하기 위해 사용 하면 풀의 tooadjust hello 크기 점진적으로 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-525">Autoscaling is not currently intended toorespond toochanges in less than a minute, but rather is intended tooadjust hello size of your pool gradually as you run a workload.</span></span>
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a><span data-ttu-id="b9713-526">기존 풀에서 자동 크기 조정 사용</span><span class="sxs-lookup"><span data-stu-id="b9713-526">Enable autoscaling on an existing pool</span></span>

<span data-ttu-id="b9713-527">각 일괄 처리 SDK 방법을 tooenable 자동 크기 조정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-527">Each Batch SDK provides a way tooenable autoscaling.</span></span> <span data-ttu-id="b9713-528">예:</span><span class="sxs-lookup"><span data-stu-id="b9713-528">For example:</span></span>

* <span data-ttu-id="b9713-529">[BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync](Batch .NET)</span><span class="sxs-lookup"><span data-stu-id="b9713-529">[BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (Batch .NET)</span></span>
* <span data-ttu-id="b9713-530">[풀에서 자동 크기 조정 사용][rest_enableautoscale] (REST API)</span><span class="sxs-lookup"><span data-stu-id="b9713-530">[Enable automatic scaling on a pool][rest_enableautoscale] (REST API)</span></span>

<span data-ttu-id="b9713-531">기존 풀에서 자동 크기 조정을 사용 하도록 설정 하면 주의 hello 지점 다음에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b9713-531">When you enable autoscaling on an existing pool, keep in mind hello following points:</span></span>

* <span data-ttu-id="b9713-532">자동 크기 조정을 현재에서 해제 되 면 hello 풀 hello 요청 tooenable 자동 크기 조정 실행 하면, hello 요청을 실행할 유효한 자동 크기 조정 수식을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-532">If automatic scaling is currently disabled on hello pool when you issue hello request tooenable autoscaling, you must specify a valid autoscale formula when you issue hello request.</span></span> <span data-ttu-id="b9713-533">필요에 따라 자동 크기 조정 평가 간격을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-533">You can optionally specify an autoscale evaluation interval.</span></span> <span data-ttu-id="b9713-534">간격을 지정 하지 않으면 hello 기본값인 15 분이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-534">If you do not specify an interval, hello default value of 15 minutes is used.</span></span>
* <span data-ttu-id="b9713-535">자동 크기 조정이 hello 풀에서 현재 사용 하는 경우에 자동 크기 조정 수식 평가 간격, 또는 둘 다 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-535">If autoscale is currently enabled on hello pool, you can specify an autoscale formula, an evaluation interval, or both.</span></span> <span data-ttu-id="b9713-536">이러한 속성 중 하나 이상을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-536">You must specify at least one of these properties.</span></span>

  * <span data-ttu-id="b9713-537">새 자동 크기 조정 평가 기간을 지정 하면 hello 기존 평가 일정 중지 되 고 새 일정을 시작 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-537">If you specify a new autoscale evaluation interval, then hello existing evaluation schedule is stopped and a new schedule is started.</span></span> <span data-ttu-id="b9713-538">hello 새 일정의 시작 시간은 hello는 hello 요청 tooenable 자동 크기 조정 발급 된 시간을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-538">hello new schedule's start time is hello time at which hello request tooenable autoscaling was issued.</span></span>
  * <span data-ttu-id="b9713-539">어느 hello 자동 크기 조정 수식 또는 계산 간격을 생략 하면 hello 일괄 처리 서비스는 hello toouse 해당 설정의 현재 값을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-539">If you omit either hello autoscale formula or evaluation interval, hello Batch service continues toouse hello current value of that setting.</span></span>

> [!NOTE]
> <span data-ttu-id="b9713-540">Hello에 대 한 값을 지정한 경우 *targetDedicatedComputeNodes* 또는 *targetLowPriorityComputeNodes* hello의 매개 변수 **CreatePool** hello를 만들 때 메서드 수식을 확장 자동 hello 계산 하는 경우.net, 또는 다른 언어를 다음 그러한 값에 hello 비교 가능한 매개 변수에 대 한 풀은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-540">If you specified values for hello *targetDedicatedComputeNodes* or *targetLowPriorityComputeNodes* parameters of hello **CreatePool** method when you created hello pool in .NET, or for hello comparable parameters in another language, then those values are ignored when hello automatic scaling formula is evaluated.</span></span>
>
>

<span data-ttu-id="b9713-541">이 C# 코드 조각은 hello를 사용 하 여 [일괄 처리.NET] [ net_api] 기존 풀에서 라이브러리 tooenable 자동 크기 조정 기능:</span><span class="sxs-lookup"><span data-stu-id="b9713-541">This C# code snippet uses hello [Batch .NET][net_api] library tooenable autoscaling on an existing pool:</span></span>

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a><span data-ttu-id="b9713-542">자동 크기 조정 수식 업데이트</span><span class="sxs-lookup"><span data-stu-id="b9713-542">Update an autoscale formula</span></span>

<span data-ttu-id="b9713-543">기존 자동 크기 조정 가능한 풀, 호출 hello 작업 tooenable 자동 크기 조정 hello 새 수식 사용 하 여 다시에서 tooupdate hello 수식입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-543">tooupdate hello formula on an existing autoscale-enabled pool, call hello operation tooenable autoscaling again with hello new formula.</span></span> <span data-ttu-id="b9713-544">예를 들어, 자동 크기 조정에서 이미 사용 되 면 `myexistingpool` hello 다음.NET 코드를 실행 하면 해당 자동 크기 조정 수식이 아래 템플릿으로 바뀝니다 hello 내용의 `myNewFormula`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-544">For example, if autoscaling is already enabled on `myexistingpool` when hello following .NET code is executed, its autoscale formula is replaced with hello contents of `myNewFormula`.</span></span>

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a><span data-ttu-id="b9713-545">업데이트 hello 자동 크기 조정 간격</span><span class="sxs-lookup"><span data-stu-id="b9713-545">Update hello autoscale interval</span></span>

<span data-ttu-id="b9713-546">hello 자동 크기 조정 평가 간격은 기존 자동 크기 조정 가능한 풀, 호출 hello 작업 tooenable 자동 크기 조정 hello 새 간격을 사용 하 여 다시의 tooupdate 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-546">tooupdate hello autoscale evaluation interval of an existing autoscale-enabled pool, call hello operation tooenable autoscaling again with hello new interval.</span></span> <span data-ttu-id="b9713-547">예를 들어 tooset hello 자동 크기 조정 평가 간격 too60 (분)는 이미.NET에서 자동 크기 조정 사용 하는 풀에:</span><span class="sxs-lookup"><span data-stu-id="b9713-547">For example, tooset hello autoscale evaluation interval too60 minutes for a pool that's already autoscale-enabled in .NET:</span></span>

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a><span data-ttu-id="b9713-548">자동 크기 조정 수식 평가</span><span class="sxs-lookup"><span data-stu-id="b9713-548">Evaluate an autoscale formula</span></span>

<span data-ttu-id="b9713-549">수식을 tooa 풀 적용 하기 전에 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-549">You can evaluate a formula before applying it tooa pool.</span></span> <span data-ttu-id="b9713-550">이러한 방식으로 hello 수식 toosee hello 수식을 프로덕션 환경에 배포 하기 전에 해당 문을 평가 하는 방법을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-550">In this way, you can test hello formula toosee how its statements evaluate before you put hello formula into production.</span></span>

<span data-ttu-id="b9713-551">자동 크기 조정 수식이 tooevaluate 먼저 유효한 수식 사용 하 여 hello 풀에서 자동 크기 조정을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-551">tooevaluate an autoscale formula, you must first enable autoscaling on hello pool with a valid formula.</span></span> <span data-ttu-id="b9713-552">tootest 아직 없는 경우 자동 크기 조정 하는 풀에 대 한 수식을 사용 하도록 설정 사용 하 여 hello 한 줄 수식을 `$TargetDedicatedNodes = 0` 자동 크기 조정 기능을 먼저 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-552">tootest a formula on a pool that doesn't yet have autoscaling enabled, use hello one-line formula `$TargetDedicatedNodes = 0` when you first enable autoscaling.</span></span> <span data-ttu-id="b9713-553">그런 다음 다음 tootest 원하는 tooevaluate hello 수식을 hello 중 하나를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-553">Then, use one of hello following tooevaluate hello formula you want tootest:</span></span>

* <span data-ttu-id="b9713-554">[BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) 또는 [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)</span><span class="sxs-lookup"><span data-stu-id="b9713-554">[BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) or [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)</span></span>

    <span data-ttu-id="b9713-555">이러한 일괄 처리.NET 메서드는 기존 풀과 hello 자동 크기 조정 수식 tooevaluate를 포함 하는 문자열의 hello ID가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-555">These Batch .NET methods require hello ID of an existing pool and a string containing hello autoscale formula tooevaluate.</span></span>

* [<span data-ttu-id="b9713-556">자동 크기 조정 수식 평가</span><span class="sxs-lookup"><span data-stu-id="b9713-556">Evaluate an automatic scaling formula</span></span>](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    <span data-ttu-id="b9713-557">이 REST API 요청 URI, hello에 hello 풀 ID를 지정 하 고 hello에 대 한 자동 크기 조정 수식을 hello *autoScaleFormula* hello 요청 본문의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-557">In this REST API request, specify hello pool ID in hello URI, and hello autoscale formula in hello *autoScaleFormula* element of hello request body.</span></span> <span data-ttu-id="b9713-558">hello 연산의 hello 응답 관련된 toohello 수식이 될 수 있는 오류 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-558">hello response of hello operation contains any error information that might be related toohello formula.</span></span>

<span data-ttu-id="b9713-559">이 [Batch .NET][net_api] 코드 조각에서는 자동 크기 조정 수식을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-559">In this [Batch .NET][net_api] code snippet, we evaluate an autoscale formula.</span></span> <span data-ttu-id="b9713-560">Hello 풀에 사용 하도록 설정 하는 자동 크기 조정 설정 여부 것 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-560">If hello pool does not have autoscaling enabled, we enable it first.</span></span>

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

<span data-ttu-id="b9713-561">이 코드 조각에 표시 하는 hello 수식의 성공적인 평가 비슷한 결과 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-561">Successful evaluation of hello formula shown in this code snippet produces results similar to:</span></span>

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a><span data-ttu-id="b9713-562">자동 크기 조정 실행에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9713-562">Get information about autoscale runs</span></span>

<span data-ttu-id="b9713-563">tooensure 수식으로 수행 하는 예상 하면 풀에 대해 일괄 처리를 수행 하는 hello 자동 크기 조정 실행의 hello 결과 주기적으로 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-563">tooensure that your formula is performing as expected, we recommend that you periodically check hello results of hello autoscaling runs that Batch performs on your pool.</span></span> <span data-ttu-id="b9713-564">toodo, get (또는 새로 고침) 참조 toohello, 풀 및 해당 마지막 자동 크기 조정 실행의 hello 속성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-564">toodo so, get (or refresh) a reference toohello pool, and examine hello properties of its last autoscale run.</span></span>

<span data-ttu-id="b9713-565">일괄 처리.net에서 hello [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) 속성에는 hello 최신 자동 크기 조정을 수행 hello 풀에서 실행 하는 방법에 대 한 정보를 제공 하는 여러 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-565">In Batch .NET, hello [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) property has several properties that provide information about hello latest automatic scaling run performed on hello pool:</span></span>

* [<span data-ttu-id="b9713-566">AutoScaleRun.Timestamp</span><span class="sxs-lookup"><span data-stu-id="b9713-566">AutoScaleRun.Timestamp</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [<span data-ttu-id="b9713-567">AutoScaleRun.Results</span><span class="sxs-lookup"><span data-stu-id="b9713-567">AutoScaleRun.Results</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [<span data-ttu-id="b9713-568">AutoScaleRun.Error</span><span class="sxs-lookup"><span data-stu-id="b9713-568">AutoScaleRun.Error</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

<span data-ttu-id="b9713-569">REST API hello에 hello [풀에 대 한 정보를 가져올](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) hello 최신 자동 크기 조정을 hello에서 실행 되는 정보를 포함 하는 hello 풀에 대 한 정보를 반환 하는 요청 [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) 속성.</span><span class="sxs-lookup"><span data-stu-id="b9713-569">In hello REST API, hello [Get information about a pool](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) request returns information about hello pool, which includes hello latest automatic scaling run information in hello [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) property.</span></span>

<span data-ttu-id="b9713-570">hello 다음 C# 코드 조각 정보 사용 하 여 hello 일괄 처리.NET 라이브러리 tooprint hello 마지막 자동 크기 조정 풀에서 실행 하는 방법에 대 한 _myPool_:</span><span class="sxs-lookup"><span data-stu-id="b9713-570">hello following C# code snippet uses hello Batch .NET library tooprint information about hello last autoscaling run on pool _myPool_:</span></span>

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

<span data-ttu-id="b9713-571">Hello 조각 앞의 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="b9713-571">Sample output of hello preceding snippet:</span></span>

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a><span data-ttu-id="b9713-572">자동 크기 조정 수식 예제</span><span class="sxs-lookup"><span data-stu-id="b9713-572">Example autoscale formulas</span></span>
<span data-ttu-id="b9713-573">풀의 계산 리소스의 다양 한 방법 tooadjust hello 크기를 표시 하는 몇 가지 수식을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-573">Let's look at a few formulas that show different ways tooadjust hello amount of compute resources in a pool.</span></span>

### <a name="example-1-time-based-adjustment"></a><span data-ttu-id="b9713-574">예제1: 시간 기반 조정</span><span class="sxs-lookup"><span data-stu-id="b9713-574">Example 1: Time-based adjustment</span></span>
<span data-ttu-id="b9713-575">Hello 요일 hello 및 하루 중 시간에 따라 tooadjust hello 풀 크기를 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-575">Suppose you want tooadjust hello pool size based on hello day of hello week and time of day.</span></span> <span data-ttu-id="b9713-576">이 예제는 hello의 노드 hello 수 tooincrease 또는 감소를 그에 따라 풀을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-576">This example shows how tooincrease or decrease hello number of nodes in hello pool accordingly.</span></span>

<span data-ttu-id="b9713-577">hello 수식은 먼저 hello를 현재 시간 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-577">hello formula first obtains hello current time.</span></span> <span data-ttu-id="b9713-578">요일 (1-5) 이면 및 작업 시간 (오전 8 시 too6 PM), hello 대상 풀 크기는 too20 노드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-578">If it's a weekday (1-5) and within working hours (8 AM too6 PM), hello target pool size is set too20 nodes.</span></span> <span data-ttu-id="b9713-579">그렇지 않으면 too10 노드는 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-579">Otherwise, it's set too10 nodes.</span></span>

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a><span data-ttu-id="b9713-580">예제2: 작업 기반 조정</span><span class="sxs-lookup"><span data-stu-id="b9713-580">Example 2: Task-based adjustment</span></span>
<span data-ttu-id="b9713-581">이 예제에서는 hello 풀 크기는 hello hello 큐에 있는 작업 수에 따라 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-581">In this example, hello pool size is adjusted based on hello number of tasks in hello queue.</span></span> <span data-ttu-id="b9713-582">주석과 줄 바꿈은 모두 수식 문자열에 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-582">Both comments and line breaks are acceptable in formula strings.</span></span>

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a><span data-ttu-id="b9713-583">예제3: 병렬 작업에 대한 회계</span><span class="sxs-lookup"><span data-stu-id="b9713-583">Example 3: Accounting for parallel tasks</span></span>
<span data-ttu-id="b9713-584">이 예제에서는 작업 hello 수에 따라 hello 풀 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-584">This example adjusts hello pool size based on hello number of tasks.</span></span> <span data-ttu-id="b9713-585">이 수식에서는 계정 hello에도 사용 [MaxTasksPerComputeNode] [ net_maxtasks] hello 풀에 대해 설정 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-585">This formula also takes into account hello [MaxTasksPerComputeNode][net_maxtasks] value that has been set for hello pool.</span></span> <span data-ttu-id="b9713-586">이 방법은 [병렬 작업 실행](batch-parallel-node-tasks.md)이 풀에서 사용된 경우에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-586">This approach is useful in situations where [parallel task execution](batch-parallel-node-tasks.md) has been enabled on your pool.</span></span>

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a><span data-ttu-id="b9713-587">예제4: 초기 풀 크기 설정</span><span class="sxs-lookup"><span data-stu-id="b9713-587">Example 4: Setting an initial pool size</span></span>
<span data-ttu-id="b9713-588">이 예제에서는 C# 코드 조각 설정 하는 자동 크기 조정 수식 사용 하 여 hello 풀 크기 tooa 초기 시간 기간에 대 한 노드 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-588">This example shows a C# code snippet with an autoscale formula that sets hello pool size tooa specified number of nodes for an initial time period.</span></span> <span data-ttu-id="b9713-589">Hello 실행 수에 따라 hello 풀 크기를 조정 하 고 hello 초기 기간 후 활성 작업 기간이 경과 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-589">Then it adjusts hello pool size based on hello number of running and active tasks after hello initial time period has elapsed.</span></span>

<span data-ttu-id="b9713-590">다음 코드 조각 hello에 hello 수식:</span><span class="sxs-lookup"><span data-stu-id="b9713-590">hello formula in hello following code snippet:</span></span>

* <span data-ttu-id="b9713-591">Hello 초기 풀 크기 toofour 노드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-591">Sets hello initial pool size toofour nodes.</span></span>
* <span data-ttu-id="b9713-592">Hello 풀 크기를 hello 내에서 처음 10 분 hello 풀의 수명 주기 조정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-592">Does not adjust hello pool size within hello first 10 minutes of hello pool's lifecycle.</span></span>
* <span data-ttu-id="b9713-593">10 분 후 hello의 최대값을 가져옵니다 hello 내에서 작업 실행 수 및 활성 hello 지난 60 분입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-593">After 10 minutes, obtains hello max value of hello number of running and active tasks within hello past 60 minutes.</span></span>
  * <span data-ttu-id="b9713-594">두 값이 0 (작업이 없는 되었는지 실행 중이거나 hello에 활성 지난 60 분을 나타냄) 인 경우 hello 풀 크기 too0을 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-594">If both values are 0 (indicating that no tasks were running or active in hello last 60 minutes), hello pool size is set too0.</span></span>
  * <span data-ttu-id="b9713-595">값 중 하나가 0보다 큰 경우 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-595">If either value is greater than zero, no change is made.</span></span>

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a><span data-ttu-id="b9713-596">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9713-596">Next steps</span></span>
* <span data-ttu-id="b9713-597">[동시 노드 작업과 Azure 배치 계산 리소스 사용량을 최대화](batch-parallel-node-tasks.md) 어떻게에 실행할 수 있습니다 여러 작업이 동시에 풀의 계산 노드 hello에 대 한 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-597">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) contains details about how you can execute multiple tasks simultaneously on hello compute nodes in your pool.</span></span> <span data-ttu-id="b9713-598">또한 tooautoscaling,이 기능은 도움이 될 수 있습니다 toolower 작업 기간을 일부 워크 로드에 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-598">In addition tooautoscaling, this feature may help toolower job duration for some workloads, saving you money.</span></span>
* <span data-ttu-id="b9713-599">다른 효율성 부스터 일괄 처리 응용 프로그램 쿼리 hello hello 최적의 방법으로 대부분의 일괄 처리 서비스는 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-599">For another efficiency booster, ensure that your Batch application queries hello Batch service in hello most optimal way.</span></span> <span data-ttu-id="b9713-600">참조 [hello Azure 배치 서비스를 효율적으로 쿼리](batch-efficient-list-queries.md) toolearn toolimit hello 잠재적으로 수천 대의 hello 상태를 쿼리할 때 hello 와이어 교차 하는 데이터 양을 방법 계산 노드 또는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b9713-600">See [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) toolearn how toolimit hello amount of data that crosses hello wire when you query hello status of potentially thousands of compute nodes or tasks.</span></span>

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
