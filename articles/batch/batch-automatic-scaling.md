---
title: "Azure 배치 풀에서 자동으로 계산 노드 크기 조정 | Microsoft Docs"
description: "클라우드 풀에서 자동 크기 조정을 사용하면 풀의 계산 노드 수를 동적으로 조정합니다."
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
ms.openlocfilehash: f0e49cd8a64a48c53f5b6104703164a597c797f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a><span data-ttu-id="4f52f-103">Batch 풀에서 계산 노드의 크기를 조정하는 자동 크기 조정 수식 만들기</span><span class="sxs-lookup"><span data-stu-id="4f52f-103">Create an automatic scaling formula for scaling compute nodes in a Batch pool</span></span>

<span data-ttu-id="4f52f-104">Azure Batch는 정의한 매개 변수에 따라 풀을 자동으로 크기 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-104">Azure Batch can automatically scale pools based on parameters that you define.</span></span> <span data-ttu-id="4f52f-105">자동 크기 조정을 사용하면 작업 요구가 증가함에 따라 Batch에서 풀에 노드를 동적으로 추가하고, 감소함에 따라 계산 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-105">With automatic scaling, Batch dynamically adds nodes to a pool as task demands increase, and removes compute nodes as they decrease.</span></span> <span data-ttu-id="4f52f-106">Batch 응용 프로그램에서 사용하는 계산 노드 수를 자동으로 조정하여 시간과 비용을 모두 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-106">You can save both time and money by automatically adjusting the number of compute nodes used by your Batch application.</span></span> 

<span data-ttu-id="4f52f-107">사용자가 정의한 *자동 크기 조정 수식*에 연결하면 계산 노드 풀에서 자동으로 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-107">You enable automatic scaling on a pool of compute nodes by associating with it an *autoscale formula* that you define.</span></span> <span data-ttu-id="4f52f-108">Batch 서비스는 자동 크기 조정 수식을 사용하여 워크로드를 실행하는 데 필요한 계산 노드의 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-108">The Batch service uses the autoscale formula to determine the number of compute nodes that are needed to execute your workload.</span></span> <span data-ttu-id="4f52f-109">계산 노드는 전용 노드이거나 [우선 순위가 낮은 노드](batch-low-pri-vms.md)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-109">Compute nodes may be dedicated nodes or [low-priority nodes](batch-low-pri-vms.md).</span></span> <span data-ttu-id="4f52f-110">Batch는 주기적으로 수집되는 서비스 메트릭 데이터에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-110">Batch responds to service metrics data that is collected periodically.</span></span> <span data-ttu-id="4f52f-111">Batch는 이 메트릭 데이터를 사용하여 구성 가능한 간격으로 수식에 따라 풀의 계산 노드 수를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-111">Using this metrics data, Batch adjusts the number of compute nodes in the pool based on your formula and at a configurable interval.</span></span>

<span data-ttu-id="4f52f-112">풀을 만들 때 또는 기존 풀에서 자동 크기 조정을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-112">You can enable automatic scaling either when a pool is created, or on an existing pool.</span></span> <span data-ttu-id="4f52f-113">자동 크기 조정에 대해 구성된 풀의 기존 수식을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-113">You can also change an existing formula on a pool that is configured for autoscaling.</span></span> <span data-ttu-id="4f52f-114">Batch를 사용하면 풀에 할당하기 전에 수식을 평가하고, 자동 크기 조정 실행 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-114">Batch enables you to evaluate your formulas before assigning them to pools and to monitor the status of automatic scaling runs.</span></span>

<span data-ttu-id="4f52f-115">이 문서에서는 변수, 연산자, 작업 및 함수를 포함하여 자동 크기 조정 수식을 구성하는 다양한 엔터티를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-115">This article discusses the various entities that make up your autoscale formulas, including variables, operators, operations, and functions.</span></span> <span data-ttu-id="4f52f-116">Batch 내의 다양한 계산 리소스 및 작업 메트릭을 가져오는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-116">We discuss how to obtain various compute resource and task metrics within Batch.</span></span> <span data-ttu-id="4f52f-117">이러한 메트릭을 사용하여 리소스 사용량과 작업 상태에 따라 풀의 노드 수를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-117">You can use these metrics to adjust your pool's node count based on resource usage and task status.</span></span> <span data-ttu-id="4f52f-118">그런 다음 Batch REST 및 .NET API를 모두 사용하여 수식을 구성하고 풀에서 자동 크기 조정을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-118">We then describe how to construct a formula and enable automatic scaling on a pool by using both the Batch REST and .NET APIs.</span></span> <span data-ttu-id="4f52f-119">마지막으로 몇 가지 예제 수식으로 마무리하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-119">Finally, we finish up with a few example formulas.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f52f-120">배치 계정을 만들 때 [계정 구성](batch-api-basics.md#account)을 지정할 수 있습니다. 이 구성은 Batch 서비스 구독(기본값) 또는 사용자 구독에 풀을 할당하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-120">When you create a Batch account, you can specify the [account configuration](batch-api-basics.md#account), which determines whether pools are allocated in a Batch service subscription (the default), or in your user subscription.</span></span> <span data-ttu-id="4f52f-121">기본 Batch 서비스 구성으로 배치 계정을 만든 경우 계정은 처리에 사용할 수 있는 코어의 최대 개수로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-121">If you created your Batch account with the default Batch Service configuration, then your account is limited to a maximum number of cores that can be used for processing.</span></span> <span data-ttu-id="4f52f-122">Batch 서비스는 계산 노드를 해당 코어 제한까지만 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-122">The Batch service scales compute nodes only up to that core limit.</span></span> <span data-ttu-id="4f52f-123">이러한 이유로 Batch 서비스는 자동 크기 조정 수식에 지정된 계산 노드의 목표 수에 도달하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-123">For this reason, the Batch service may not reach the target number of compute nodes specified by an autoscale formula.</span></span> <span data-ttu-id="4f52f-124">계정 할당량을 보고 늘리는 방법에 대한 내용은 [Azure 배치 서비스에 대한 할당량 및 제한](batch-quota-limit.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f52f-124">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for information on viewing and increasing your account quotas.</span></span>
>
><span data-ttu-id="4f52f-125">사용자 구독 구성으로 계정을 만든 경우 계정은 구독의 코어 할당량을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-125">If you created your account with the User Subscription configuration, then your account shares in the core quota for the subscription.</span></span> <span data-ttu-id="4f52f-126">자세한 내용은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)에서 [Virtual Machines 제한](../azure-subscription-service-limits.md#virtual-machines-limits)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f52f-126">For more information, see [Virtual Machines limits](../azure-subscription-service-limits.md#virtual-machines-limits) in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
>
>

## <a name="automatic-scaling-formulas"></a><span data-ttu-id="4f52f-127">자동 크기 조정 수식</span><span class="sxs-lookup"><span data-stu-id="4f52f-127">Automatic scaling formulas</span></span>
<span data-ttu-id="4f52f-128">자동 크기 조정 수식은 하나 이상의 문을 포함하는 사용자가 정의한 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-128">An automatic scaling formula is a string value that you define that contains one or more statements.</span></span> <span data-ttu-id="4f52f-129">자동 크기 조정 수식은 풀의 [autoScaleFormula][rest_autoscaleformula] 요소(Batch REST) 또는 [CloudPool.AutoScaleFormula][net_cloudpool_autoscaleformula] 속성(Batch .NET)에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-129">The autoscale formula is assigned to a pool's [autoScaleFormula][rest_autoscaleformula] element (Batch REST) or [CloudPool.AutoScaleFormula][net_cloudpool_autoscaleformula] property (Batch .NET).</span></span> <span data-ttu-id="4f52f-130">Batch 서비스는 처리할 다음 간격을 위해 풀의 대상 계산 노드 수를 결정하는 수식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-130">The Batch service uses your formula to determine the target number of compute nodes in the pool for the next interval of processing.</span></span> <span data-ttu-id="4f52f-131">수식 문자열은 8KB를 초과할 수 없고, 세미콜론으로 구분된 구문을 100개까지 포함할 수 있으며, 줄 바꿈과 주석을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-131">The formula string cannot exceed 8 KB, can include up to 100 statements that are separated by semicolons, and can include line breaks and comments.</span></span>

<span data-ttu-id="4f52f-132">자동 크기 조정 수식은 Batch 자동 크기 조정 "언어"로 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-132">You can think of automatic scaling formulas as a Batch autoscale "language."</span></span> <span data-ttu-id="4f52f-133">수식 문은 자유 형식이고 서비스가 정의한 변수(배치 서비스에 의해 정의된 변수) 및 사용자가 정의한 변수(사용자가 정의한 변수)를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-133">Formula statements are free-formed expressions that can include both service-defined variables (variables defined by the Batch service) and user-defined variables (variables that you define).</span></span> <span data-ttu-id="4f52f-134">기본 제공 형식, 연산자 및 함수를 사용하여 이러한 값에 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-134">They can perform various operations on these values by using built-in types, operators, and functions.</span></span> <span data-ttu-id="4f52f-135">예를 들어 문은 다음과 같은 형태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-135">For example, a statement might take the following form:</span></span>

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

<span data-ttu-id="4f52f-136">수식은 일반적으로 이전 문에서 가져온 값에 대한 작업을 수행하는 여러 문을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-136">Formulas generally contain multiple statements that perform operations on values that are obtained in previous statements.</span></span> <span data-ttu-id="4f52f-137">예를 들어 먼저 `variable1`에 대한 값을 구한 다음 `variable2`을(를) 채우는 함수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-137">For example, first we obtain a value for `variable1`, then pass it to a function to populate `variable2`:</span></span>

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

<span data-ttu-id="4f52f-138">자동 크기 조정 수식에 이러한 문을 포함하여 계산 노드의 목표 수에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-138">Include these statements in your autoscale formula to arrive at a target number of compute nodes.</span></span> <span data-ttu-id="4f52f-139">전용 노드와 우선 순위가 낮은 노드에는 각각 자체의 목표 설정이 있으므로 각 노드 형식의 목표를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-139">Dedicated nodes and low-priority nodes each have their own target settings, so that you can define a target for each type of node.</span></span> <span data-ttu-id="4f52f-140">자동 크기 조정 수식에는 전용 노드의 목표 값, 우선 순위가 낮은 노드의 목표 값 또는 둘 다가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-140">An autoscale formula can include a target value for dedicated nodes, a target value for low-priority nodes, or both.</span></span>

<span data-ttu-id="4f52f-141">노드의 목표 수는 풀에 있는 해당 노드 형식의 현재 수보다 높거나, 낮거나, 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-141">The target number of nodes may be higher, lower, or the same as the current number of nodes of that type in the pool.</span></span> <span data-ttu-id="4f52f-142">Batch는 풀의 자동 크기 조정 수식을 특정 간격([자동 크기 조정 간격](#automatic-scaling-interval) 참조)으로 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-142">Batch evaluates a pool's autoscale formula at a specific interval (see [automatic scaling intervals](#automatic-scaling-interval)).</span></span> <span data-ttu-id="4f52f-143">Batch는 풀에 있는 각 노드 형식의 목표 수를 크기 조정 수식에서 평가할 때 지정하는 수로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-143">Batch adjusts the target number of each type of node in the pool to the number that your autoscale formula specifies at the time of evaluation.</span></span>

### <a name="sample-autoscale-formula"></a><span data-ttu-id="4f52f-144">샘플 자동 크기 조정 수식</span><span class="sxs-lookup"><span data-stu-id="4f52f-144">Sample autoscale formula</span></span>

<span data-ttu-id="4f52f-145">다음은 대부분의 시나리오에 맞게 조정할 수 있는 자동 크기 조정 수식의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-145">Here is an example of an autoscale formula that can be adjusted to work for most scenarios.</span></span> <span data-ttu-id="4f52f-146">예제 수식에서 변수 `startingNumberOfVMs` 및 `maxNumberofVMs`는 필요에 따라 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-146">The variables `startingNumberOfVMs` and `maxNumberofVMs` in the example formula can be adjusted to your needs.</span></span> <span data-ttu-id="4f52f-147">이 수식은 전용 노드를 크기 조정하지만 우선 순위가 낮은 노드를 크기 조정하는 데 적용되도록 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-147">This formula scales dedicated nodes, but can be modified to apply to scale low-priority nodes as well.</span></span> 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

<span data-ttu-id="4f52f-148">이 자동 크기 조정 수식을 사용하면 풀은 단일 VM으로 처음에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-148">With this autoscale formula, the pool is initially created with a single VM.</span></span> <span data-ttu-id="4f52f-149">`$PendingTasks` 메트릭은 실행 중이거나 큐에 대기 중인 작업의 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-149">The `$PendingTasks` metric defines the number of tasks that are running or queued.</span></span> <span data-ttu-id="4f52f-150">수식은 지난 180초 동안 보류 중인 작업의 평균 수를 찾고 이에 따라 `$TargetDedicatedNodes` 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-150">The formula finds the average number of pending tasks in the last 180 seconds and sets the `$TargetDedicatedNodes` variable accordingly.</span></span> <span data-ttu-id="4f52f-151">수식은 전용 노드의 목표 수가 25개 VM을 절대로 초과하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-151">The formula ensures that the target number of dedicated nodes never exceeds 25 VMs.</span></span> <span data-ttu-id="4f52f-152">새 작업이 제출되면 풀은 자동으로 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-152">As new tasks are submitted, the pool automatically grows.</span></span> <span data-ttu-id="4f52f-153">작업이 완료되면 VM은 하나씩 비워지고 자동 크기 조정 수식은 풀을 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-153">As tasks complete, VMs become free one by one and the autoscaling formula shrinks the pool.</span></span>

## <a name="variables"></a><span data-ttu-id="4f52f-154">variables</span><span class="sxs-lookup"><span data-stu-id="4f52f-154">Variables</span></span>
<span data-ttu-id="4f52f-155">자동 크기 조정 수식에는 **서비스 정의** 및 **사용자 정의** 변수를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-155">You can use both **service-defined** and **user-defined** variables in your autoscale formulas.</span></span> <span data-ttu-id="4f52f-156">서비스 정의 변수는 Batch 서비스에 기본 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-156">The service-defined variables are built in to the Batch service.</span></span> <span data-ttu-id="4f52f-157">서비스 정의 변수 일부는 읽기-쓰기이고, 일부는 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-157">Some service-defined variables are read-write, and some are read-only.</span></span> <span data-ttu-id="4f52f-158">사용자 정의 변수는 사용자가 정의한 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-158">User-defined variables are variables that you define.</span></span> <span data-ttu-id="4f52f-159">이전 섹션에 나온 예제 수식에서 `$TargetDedicatedNodes` 및 `$PendingTasks`는 서비스 정의 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-159">In the example formula shown in the previous section, `$TargetDedicatedNodes` and `$PendingTasks` are service-defined variables.</span></span> <span data-ttu-id="4f52f-160">변수 `startingNumberOfVMs` 및 `maxNumberofVMs`는 사용자 정의 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-160">Variables `startingNumberOfVMs` and `maxNumberofVMs` are user-defined variables.</span></span>

> [!NOTE]
> <span data-ttu-id="4f52f-161">서비스 정의 변수에는 항상 달러($) 기호가 앞에 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-161">Service-defined variables are always preceded by a dollar sign ($).</span></span> <span data-ttu-id="4f52f-162">사용자 정의 변수의 경우 달러 기호는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-162">For user-defined variables, the dollar sign is optional.</span></span>
>
>

<span data-ttu-id="4f52f-163">아래 표에서는 Batch 서비스에서 정의하는 읽기-쓰기 및 읽기 전용 변수를 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-163">The following tables show both read-write and read-only variables that are defined by the Batch service.</span></span>

<span data-ttu-id="4f52f-164">다음과 같은 서비스 정의 변수의 값을 가져오고 설정하여 풀의 계산 노드 수를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-164">You can get and set the values of these service-defined variables to manage the number of compute nodes in a pool:</span></span>

| <span data-ttu-id="4f52f-165">읽기-쓰기 서비스 정의 변수</span><span class="sxs-lookup"><span data-stu-id="4f52f-165">Read-write service-defined variables</span></span> | <span data-ttu-id="4f52f-166">설명</span><span class="sxs-lookup"><span data-stu-id="4f52f-166">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f52f-167">$TargetDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="4f52f-167">$TargetDedicatedNodes</span></span> |<span data-ttu-id="4f52f-168">풀에 대한 전용 계산 노드의 목표 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-168">The target number of dedicated compute nodes for the pool.</span></span> <span data-ttu-id="4f52f-169">풀에서 항상 원하는 수의 노드에 도달할 수 없으므로 전용 노드의 수가 목표 수로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-169">The number of dedicated nodes is specified as a target because a pool may not always achieve the desired number of nodes.</span></span> <span data-ttu-id="4f52f-170">예를 들어 풀에서 최초 목표에 도달하기 전에 자동 크기 조정 평가에 따라 전용 노드의 목표 수가 수정되는 경우 풀에서 목표에 도달하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-170">For example, if the target number of dedicated nodes is modified by an autoscale evaluation before the pool has reached the initial target, then the pool may not reach the target.</span></span> <br /><br /> <span data-ttu-id="4f52f-171">목표가 배치 계정 노드 또는 코어 할당량을 초과하는 경우 Batch 서비스 구성으로 만든 계정의 풀에서 해당 목표에 도달하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-171">A pool in an account created with the Batch Service configuration may not achieve its target if the target exceeds a Batch account node or core quota.</span></span> <span data-ttu-id="4f52f-172">목표가 구독의 공유 코어 할당량을 초과하는 경우 사용자 구독 구성으로 만든 계정의 풀에서 해당 목표에 도달하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-172">A pool in an account created with the User Subscription configuration may not achieve its target if the target exceeds the shared core quota for the subscription.</span></span>|
| <span data-ttu-id="4f52f-173">$TargetLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="4f52f-173">$TargetLowPriorityNodes</span></span> |<span data-ttu-id="4f52f-174">풀에 대한 우선 순위가 낮은 계산 노드의 목표 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-174">The target number of low-priority compute nodes for the pool.</span></span> <span data-ttu-id="4f52f-175">풀에서 항상 원하는 수의 노드에 도달할 수 없으므로 우선 순위가 낮은 노드의 수가 목표 수로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-175">The number of low-priority nodes is specified as a target because a pool may not always achieve the desired number of nodes.</span></span> <span data-ttu-id="4f52f-176">예를 들어 풀에서 최초 목표에 도달하기 전에 자동 크기 조정 평가에 따라 우선 순위가 낮은 노드의 목표 수가 수정되는 경우 풀에서 목표에 도달하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-176">For example, if the target number of low-priority nodes is modified by an autoscale evaluation before the pool has reached the initial target, then the pool may not reach the target.</span></span> <span data-ttu-id="4f52f-177">목표가 배치 계정 노드 또는 코어 할당량을 초과하는 경우 풀에서 해당 목표에 도달하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-177">A pool may also not achieve its target if the target exceeds a Batch account node or core quota.</span></span> <br /><br /> <span data-ttu-id="4f52f-178">우선 순위가 낮은 계산 노드에 대한 자세한 내용은 [Batch(미리 보기)에서 낮은 우선 순위 VM 사용](batch-low-pri-vms.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f52f-178">For more information on low-priority compute nodes, see [Use low-priority VMs with Batch (Preview)](batch-low-pri-vms.md).</span></span> |
| <span data-ttu-id="4f52f-179">$NodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="4f52f-179">$NodeDeallocationOption</span></span> |<span data-ttu-id="4f52f-180">풀에서 계산 노드가 제거되는 경우 발생하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-180">The action that occurs when compute nodes are removed from a pool.</span></span> <span data-ttu-id="4f52f-181">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-181">Possible values are:</span></span><ul><li><span data-ttu-id="4f52f-182">**requeue** - 태스크를 즉시 종료하고 일정을 재조정하도록 작업 큐에 다시 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-182">**requeue**--Terminates tasks immediately and puts them back on the job queue so that they are rescheduled.</span></span><li><span data-ttu-id="4f52f-183">**terminate** - 태스크를 즉시 종료하고 작업 큐에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-183">**terminate**--Terminates tasks immediately and removes them from the job queue.</span></span><li><span data-ttu-id="4f52f-184">**taskcompletion** - 현재 실행 중인 태스크가 완료되기를 기다린 다음 풀에서 해당 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-184">**taskcompletion**--Waits for currently running tasks to finish and then removes the node from the pool.</span></span><li><span data-ttu-id="4f52f-185">**retaineddata** - 노드의 모든 로컬 태스크 보유 데이터가 정리되기를 기다린 다음 풀에서 해당 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-185">**retaineddata**--Waits for all the local task-retained data on the node to be cleaned up before removing the node from the pool.</span></span></ul> |

<span data-ttu-id="4f52f-186">이러한 서비스 정의 변수의 값을 가져와서 Batch 서비스의 메트릭을 기반으로 하여 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-186">You can get the value of these service-defined variables to make adjustments that are based on metrics from the Batch service:</span></span>

| <span data-ttu-id="4f52f-187">읽기 전용 서비스 정의 변수</span><span class="sxs-lookup"><span data-stu-id="4f52f-187">Read-only service-defined variables</span></span> | <span data-ttu-id="4f52f-188">설명</span><span class="sxs-lookup"><span data-stu-id="4f52f-188">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f52f-189">$CPUPercent</span><span class="sxs-lookup"><span data-stu-id="4f52f-189">$CPUPercent</span></span> |<span data-ttu-id="4f52f-190">평균 CPU 사용량 비율.</span><span class="sxs-lookup"><span data-stu-id="4f52f-190">The average percentage of CPU usage.</span></span> |
| <span data-ttu-id="4f52f-191">$WallClockSeconds</span><span class="sxs-lookup"><span data-stu-id="4f52f-191">$WallClockSeconds</span></span> |<span data-ttu-id="4f52f-192">사용된 시간(초) 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-192">The number of seconds consumed.</span></span> |
| <span data-ttu-id="4f52f-193">$MemoryBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-193">$MemoryBytes</span></span> |<span data-ttu-id="4f52f-194">사용된 평균 메가바이트 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-194">The average number of megabytes used.</span></span> |
| <span data-ttu-id="4f52f-195">$DiskBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-195">$DiskBytes</span></span> |<span data-ttu-id="4f52f-196">로컬 디스크에서 사용된 평균 기가바이트 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-196">The average number of gigabytes used on the local disks.</span></span> |
| <span data-ttu-id="4f52f-197">$DiskReadBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-197">$DiskReadBytes</span></span> |<span data-ttu-id="4f52f-198">읽은 바이트 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-198">The number of bytes read.</span></span> |
| <span data-ttu-id="4f52f-199">$DiskWriteBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-199">$DiskWriteBytes</span></span> |<span data-ttu-id="4f52f-200">쓴 바이트 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-200">The number of bytes written.</span></span> |
| <span data-ttu-id="4f52f-201">$DiskReadOps</span><span class="sxs-lookup"><span data-stu-id="4f52f-201">$DiskReadOps</span></span> |<span data-ttu-id="4f52f-202">수행된 디스크 읽기 작업 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-202">The count of read disk operations performed.</span></span> |
| <span data-ttu-id="4f52f-203">$DiskWriteOps</span><span class="sxs-lookup"><span data-stu-id="4f52f-203">$DiskWriteOps</span></span> |<span data-ttu-id="4f52f-204">수행된 디스크 쓰기 작업 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-204">The count of write disk operations performed.</span></span> |
| <span data-ttu-id="4f52f-205">$NetworkInBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-205">$NetworkInBytes</span></span> |<span data-ttu-id="4f52f-206">인바운드 바이트 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-206">The number of inbound bytes.</span></span> |
| <span data-ttu-id="4f52f-207">$NetworkOutBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-207">$NetworkOutBytes</span></span> |<span data-ttu-id="4f52f-208">아웃바운드 바이트 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-208">The number of outbound bytes.</span></span> |
| <span data-ttu-id="4f52f-209">$SampleNodeCount</span><span class="sxs-lookup"><span data-stu-id="4f52f-209">$SampleNodeCount</span></span> |<span data-ttu-id="4f52f-210">계산 노드 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-210">The count of compute nodes.</span></span> |
| <span data-ttu-id="4f52f-211">$ActiveTasks</span><span class="sxs-lookup"><span data-stu-id="4f52f-211">$ActiveTasks</span></span> |<span data-ttu-id="4f52f-212">실행할 준비가 되었지만 아직 실행되지 않은 작업 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-212">The number of tasks that are ready to execute but are not yet executing.</span></span> <span data-ttu-id="4f52f-213">$ActiveTasks 수에는 활성 상태에 있고 종속성이 충족된 작업이 모두 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-213">The $ActiveTasks count includes all tasks that are in the active state and whose dependencies have been satisfied.</span></span> <span data-ttu-id="4f52f-214">활성 상태이지만 종속성이 충족되지 않은 작업은 모두 $ActiveTasks 수에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-214">Any tasks that are in the active state but whose dependencies have not been satisfied are excluded from the $ActiveTasks count.</span></span>|
| <span data-ttu-id="4f52f-215">$RunningTasks</span><span class="sxs-lookup"><span data-stu-id="4f52f-215">$RunningTasks</span></span> |<span data-ttu-id="4f52f-216">실행 중 상태인 태스크 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-216">The number of tasks in a running state.</span></span> |
| <span data-ttu-id="4f52f-217">$PendingTasks</span><span class="sxs-lookup"><span data-stu-id="4f52f-217">$PendingTasks</span></span> |<span data-ttu-id="4f52f-218">$ActiveTasks 및 $RunningTasks의 합입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-218">The sum of $ActiveTasks and $RunningTasks.</span></span> |
| <span data-ttu-id="4f52f-219">$SucceededTasks</span><span class="sxs-lookup"><span data-stu-id="4f52f-219">$SucceededTasks</span></span> |<span data-ttu-id="4f52f-220">성공적으로 완료된 태스크 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-220">The number of tasks that finished successfully.</span></span> |
| <span data-ttu-id="4f52f-221">$FailedTasks</span><span class="sxs-lookup"><span data-stu-id="4f52f-221">$FailedTasks</span></span> |<span data-ttu-id="4f52f-222">실패한 태스크 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-222">The number of tasks that failed.</span></span> |
| <span data-ttu-id="4f52f-223">$CurrentDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="4f52f-223">$CurrentDedicatedNodes</span></span> |<span data-ttu-id="4f52f-224">현재 전용 계산 노드 수.</span><span class="sxs-lookup"><span data-stu-id="4f52f-224">The current number of dedicated compute nodes.</span></span> |
| <span data-ttu-id="4f52f-225">$CurrentLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="4f52f-225">$CurrentLowPriorityNodes</span></span> |<span data-ttu-id="4f52f-226">선점된 노드를 포함하여 우선 순위가 낮은 계산 노드의 현재 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-226">The current number of low-priority compute nodes, including any nodes that have been pre-empted.</span></span> |
| <span data-ttu-id="4f52f-227">$PreemptedNodeCount</span><span class="sxs-lookup"><span data-stu-id="4f52f-227">$PreemptedNodeCount</span></span> | <span data-ttu-id="4f52f-228">선점 상태에 있는 풀의 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-228">The number of nodes in the pool that are in a pre-empted state.</span></span> |

> [!TIP]
> <span data-ttu-id="4f52f-229">앞의 표에서 설명하는 읽기 전용 서비스 정의 변수는 각각에 연결된 데이터에 액세스하는 다양한 메서드를 제공하는 *개체*입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-229">The read-only, service-defined variables that are shown in the previous table are *objects* that provide various methods to access data associated with each.</span></span> <span data-ttu-id="4f52f-230">자세한 내용은 이 문서의 뒷부분에 나오는 [샘플 데이터 가져오기](#getsampledata)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f52f-230">For more information, see [Obtain sample data](#getsampledata) later in this article.</span></span>
>
>

## <a name="types"></a><span data-ttu-id="4f52f-231">형식</span><span class="sxs-lookup"><span data-stu-id="4f52f-231">Types</span></span>
<span data-ttu-id="4f52f-232">수식에 지원되는 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-232">These types are supported in a formula:</span></span>

* <span data-ttu-id="4f52f-233">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-233">double</span></span>
* <span data-ttu-id="4f52f-234">doubleVec</span><span class="sxs-lookup"><span data-stu-id="4f52f-234">doubleVec</span></span>
* <span data-ttu-id="4f52f-235">doubleVecList</span><span class="sxs-lookup"><span data-stu-id="4f52f-235">doubleVecList</span></span>
* <span data-ttu-id="4f52f-236">string</span><span class="sxs-lookup"><span data-stu-id="4f52f-236">string</span></span>
* <span data-ttu-id="4f52f-237">timestamp--타임스탬프는 다음의 멤버를 포함하는 복합 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-237">timestamp--timestamp is a compound structure that contains the following members:</span></span>

  * <span data-ttu-id="4f52f-238">year</span><span class="sxs-lookup"><span data-stu-id="4f52f-238">year</span></span>
  * <span data-ttu-id="4f52f-239">month (1-12)</span><span class="sxs-lookup"><span data-stu-id="4f52f-239">month (1-12)</span></span>
  * <span data-ttu-id="4f52f-240">day (1-31)</span><span class="sxs-lookup"><span data-stu-id="4f52f-240">day (1-31)</span></span>
  * <span data-ttu-id="4f52f-241">weekday(숫자 형식, 예: 1은 월요일을 의미함)</span><span class="sxs-lookup"><span data-stu-id="4f52f-241">weekday (in the format of number; for example, 1 for Monday)</span></span>
  * <span data-ttu-id="4f52f-242">hour(24시간 형식, 예: 13은 오후 1시를 의미함)</span><span class="sxs-lookup"><span data-stu-id="4f52f-242">hour (in 24-hour number format; for example, 13 means 1 PM)</span></span>
  * <span data-ttu-id="4f52f-243">minute (00-59)</span><span class="sxs-lookup"><span data-stu-id="4f52f-243">minute (00-59)</span></span>
  * <span data-ttu-id="4f52f-244">second (00-59)</span><span class="sxs-lookup"><span data-stu-id="4f52f-244">second (00-59)</span></span>
* <span data-ttu-id="4f52f-245">timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-245">timeinterval</span></span>

  * <span data-ttu-id="4f52f-246">TimeInterval_Zero</span><span class="sxs-lookup"><span data-stu-id="4f52f-246">TimeInterval_Zero</span></span>
  * <span data-ttu-id="4f52f-247">TimeInterval_100ns</span><span class="sxs-lookup"><span data-stu-id="4f52f-247">TimeInterval_100ns</span></span>
  * <span data-ttu-id="4f52f-248">TimeInterval_Microsecond</span><span class="sxs-lookup"><span data-stu-id="4f52f-248">TimeInterval_Microsecond</span></span>
  * <span data-ttu-id="4f52f-249">TimeInterval_Millisecond</span><span class="sxs-lookup"><span data-stu-id="4f52f-249">TimeInterval_Millisecond</span></span>
  * <span data-ttu-id="4f52f-250">TimeInterval_Second</span><span class="sxs-lookup"><span data-stu-id="4f52f-250">TimeInterval_Second</span></span>
  * <span data-ttu-id="4f52f-251">TimeInterval_Minute</span><span class="sxs-lookup"><span data-stu-id="4f52f-251">TimeInterval_Minute</span></span>
  * <span data-ttu-id="4f52f-252">TimeInterval_Hour</span><span class="sxs-lookup"><span data-stu-id="4f52f-252">TimeInterval_Hour</span></span>
  * <span data-ttu-id="4f52f-253">TimeInterval_Day</span><span class="sxs-lookup"><span data-stu-id="4f52f-253">TimeInterval_Day</span></span>
  * <span data-ttu-id="4f52f-254">TimeInterval_Week</span><span class="sxs-lookup"><span data-stu-id="4f52f-254">TimeInterval_Week</span></span>
  * <span data-ttu-id="4f52f-255">TimeInterval_Year</span><span class="sxs-lookup"><span data-stu-id="4f52f-255">TimeInterval_Year</span></span>

## <a name="operations"></a><span data-ttu-id="4f52f-256">작업</span><span class="sxs-lookup"><span data-stu-id="4f52f-256">Operations</span></span>
<span data-ttu-id="4f52f-257">이전 섹션에서 나열된 형식에서 허용되는 연산은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-257">These operations are allowed on the types that are listed in the previous section.</span></span>

| <span data-ttu-id="4f52f-258">작업</span><span class="sxs-lookup"><span data-stu-id="4f52f-258">Operation</span></span> | <span data-ttu-id="4f52f-259">지원되는 연산자</span><span class="sxs-lookup"><span data-stu-id="4f52f-259">Supported operators</span></span> | <span data-ttu-id="4f52f-260">결과 형식</span><span class="sxs-lookup"><span data-stu-id="4f52f-260">Result type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f52f-261">double *operator* double</span><span class="sxs-lookup"><span data-stu-id="4f52f-261">double *operator* double</span></span> |<span data-ttu-id="4f52f-262">+, -, *, /</span><span class="sxs-lookup"><span data-stu-id="4f52f-262">+, -, *, /</span></span> |<span data-ttu-id="4f52f-263">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-263">double</span></span> |
| <span data-ttu-id="4f52f-264">double *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-264">double *operator* timeinterval</span></span> |* |<span data-ttu-id="4f52f-265">timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-265">timeinterval</span></span> |
| <span data-ttu-id="4f52f-266">doubleVec *operator* double</span><span class="sxs-lookup"><span data-stu-id="4f52f-266">doubleVec *operator* double</span></span> |<span data-ttu-id="4f52f-267">+, -, *, /</span><span class="sxs-lookup"><span data-stu-id="4f52f-267">+, -, *, /</span></span> |<span data-ttu-id="4f52f-268">doubleVec</span><span class="sxs-lookup"><span data-stu-id="4f52f-268">doubleVec</span></span> |
| <span data-ttu-id="4f52f-269">doubleVec *operator* doubleVec</span><span class="sxs-lookup"><span data-stu-id="4f52f-269">doubleVec *operator* doubleVec</span></span> |<span data-ttu-id="4f52f-270">+, -, *, /</span><span class="sxs-lookup"><span data-stu-id="4f52f-270">+, -, *, /</span></span> |<span data-ttu-id="4f52f-271">doubleVec</span><span class="sxs-lookup"><span data-stu-id="4f52f-271">doubleVec</span></span> |
| <span data-ttu-id="4f52f-272">timeinterval *operator* double</span><span class="sxs-lookup"><span data-stu-id="4f52f-272">timeinterval *operator* double</span></span> |<span data-ttu-id="4f52f-273">*, /</span><span class="sxs-lookup"><span data-stu-id="4f52f-273">*, /</span></span> |<span data-ttu-id="4f52f-274">timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-274">timeinterval</span></span> |
| <span data-ttu-id="4f52f-275">timeinterval *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-275">timeinterval *operator* timeinterval</span></span> |<span data-ttu-id="4f52f-276">+, -</span><span class="sxs-lookup"><span data-stu-id="4f52f-276">+, -</span></span> |<span data-ttu-id="4f52f-277">timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-277">timeinterval</span></span> |
| <span data-ttu-id="4f52f-278">timeinterval *operator* timestamp</span><span class="sxs-lookup"><span data-stu-id="4f52f-278">timeinterval *operator* timestamp</span></span> |+ |<span data-ttu-id="4f52f-279">timestamp</span><span class="sxs-lookup"><span data-stu-id="4f52f-279">timestamp</span></span> |
| <span data-ttu-id="4f52f-280">timestamp *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-280">timestamp *operator* timeinterval</span></span> |+ |<span data-ttu-id="4f52f-281">timestamp</span><span class="sxs-lookup"><span data-stu-id="4f52f-281">timestamp</span></span> |
| <span data-ttu-id="4f52f-282">timestamp *operator* timestamp</span><span class="sxs-lookup"><span data-stu-id="4f52f-282">timestamp *operator* timestamp</span></span> |- |<span data-ttu-id="4f52f-283">timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-283">timeinterval</span></span> |
| <span data-ttu-id="4f52f-284">*operator*double</span><span class="sxs-lookup"><span data-stu-id="4f52f-284">*operator*double</span></span> |<span data-ttu-id="4f52f-285">-, !</span><span class="sxs-lookup"><span data-stu-id="4f52f-285">-, !</span></span> |<span data-ttu-id="4f52f-286">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-286">double</span></span> |
| <span data-ttu-id="4f52f-287">*operator*timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-287">*operator*timeinterval</span></span> |- |<span data-ttu-id="4f52f-288">timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-288">timeinterval</span></span> |
| <span data-ttu-id="4f52f-289">double *operator* double</span><span class="sxs-lookup"><span data-stu-id="4f52f-289">double *operator* double</span></span> |<span data-ttu-id="4f52f-290"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="4f52f-290"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="4f52f-291">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-291">double</span></span> |
| <span data-ttu-id="4f52f-292">string *operator* string</span><span class="sxs-lookup"><span data-stu-id="4f52f-292">string *operator* string</span></span> |<span data-ttu-id="4f52f-293"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="4f52f-293"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="4f52f-294">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-294">double</span></span> |
| <span data-ttu-id="4f52f-295">timestamp *operator* timestamp</span><span class="sxs-lookup"><span data-stu-id="4f52f-295">timestamp *operator* timestamp</span></span> |<span data-ttu-id="4f52f-296"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="4f52f-296"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="4f52f-297">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-297">double</span></span> |
| <span data-ttu-id="4f52f-298">timeinterval *operator* timeinterval</span><span class="sxs-lookup"><span data-stu-id="4f52f-298">timeinterval *operator* timeinterval</span></span> |<span data-ttu-id="4f52f-299"><, <=, ==, >=, >, !=</span><span class="sxs-lookup"><span data-stu-id="4f52f-299"><, <=, ==, >=, >, !=</span></span> |<span data-ttu-id="4f52f-300">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-300">double</span></span> |
| <span data-ttu-id="4f52f-301">double *operator* double</span><span class="sxs-lookup"><span data-stu-id="4f52f-301">double *operator* double</span></span> |<span data-ttu-id="4f52f-302">&&, &#124;&#124;</span><span class="sxs-lookup"><span data-stu-id="4f52f-302">&&, &#124;&#124;</span></span> |<span data-ttu-id="4f52f-303">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-303">double</span></span> |

<span data-ttu-id="4f52f-304">3항 연산자(`double ? statement1 : statement2`)가 있는 이중 연산자를 테스트할 경우 0이 아님이 **true**이고 0은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-304">When testing a double with a ternary operator (`double ? statement1 : statement2`), nonzero is **true**, and zero is **false**.</span></span>

## <a name="functions"></a><span data-ttu-id="4f52f-305">함수</span><span class="sxs-lookup"><span data-stu-id="4f52f-305">Functions</span></span>
<span data-ttu-id="4f52f-306">이러한 미리 정의된 **함수** 는 자동 크기 조정 수식을 정의하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-306">These predefined **functions** are available for you to use in defining an automatic scaling formula.</span></span>

| <span data-ttu-id="4f52f-307">함수</span><span class="sxs-lookup"><span data-stu-id="4f52f-307">Function</span></span> | <span data-ttu-id="4f52f-308">반환 형식</span><span class="sxs-lookup"><span data-stu-id="4f52f-308">Return type</span></span> | <span data-ttu-id="4f52f-309">설명</span><span class="sxs-lookup"><span data-stu-id="4f52f-309">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f52f-310">avg(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-310">avg(doubleVecList)</span></span> |<span data-ttu-id="4f52f-311">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-311">double</span></span> |<span data-ttu-id="4f52f-312">doubleVecList에 있는 모든 값의 평균 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-312">Returns the average value for all values in the doubleVecList.</span></span> |
| <span data-ttu-id="4f52f-313">len(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-313">len(doubleVecList)</span></span> |<span data-ttu-id="4f52f-314">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-314">double</span></span> |<span data-ttu-id="4f52f-315">doubleVecList에서 만든 벡터의 길이를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-315">Returns the length of the vector that is created from the doubleVecList.</span></span> |
| <span data-ttu-id="4f52f-316">lg(double)</span><span class="sxs-lookup"><span data-stu-id="4f52f-316">lg(double)</span></span> |<span data-ttu-id="4f52f-317">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-317">double</span></span> |<span data-ttu-id="4f52f-318">double의 로그 밑 2를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-318">Returns the log base 2 of the double.</span></span> |
| <span data-ttu-id="4f52f-319">lg(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-319">lg(doubleVecList)</span></span> |<span data-ttu-id="4f52f-320">doubleVec</span><span class="sxs-lookup"><span data-stu-id="4f52f-320">doubleVec</span></span> |<span data-ttu-id="4f52f-321">doubleVecList의 구성 요소 로그 밑 2를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-321">Returns the component-wise log base 2 of the doubleVecList.</span></span> <span data-ttu-id="4f52f-322">vec(double)은 매개 변수에 대해 명시적으로 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-322">A vec(double) must be explicitly passed for the parameter.</span></span> <span data-ttu-id="4f52f-323">그렇지 않으면 double lg(double) 버전으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-323">Otherwise, the double lg(double) version is assumed.</span></span> |
| <span data-ttu-id="4f52f-324">ln(double)</span><span class="sxs-lookup"><span data-stu-id="4f52f-324">ln(double)</span></span> |<span data-ttu-id="4f52f-325">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-325">double</span></span> |<span data-ttu-id="4f52f-326">double의 자연 로그를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-326">Returns the natural log of the double.</span></span> |
| <span data-ttu-id="4f52f-327">ln(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-327">ln(doubleVecList)</span></span> |<span data-ttu-id="4f52f-328">doubleVec</span><span class="sxs-lookup"><span data-stu-id="4f52f-328">doubleVec</span></span> |<span data-ttu-id="4f52f-329">doubleVecList의 구성 요소 로그 밑 2를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-329">Returns the component-wise log base 2 of the doubleVecList.</span></span> <span data-ttu-id="4f52f-330">vec(double)은 매개 변수에 대해 명시적으로 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-330">A vec(double) must be explicitly passed for the parameter.</span></span> <span data-ttu-id="4f52f-331">그렇지 않으면 double lg(double) 버전으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-331">Otherwise, the double lg(double) version is assumed.</span></span> |
| <span data-ttu-id="4f52f-332">log(double)</span><span class="sxs-lookup"><span data-stu-id="4f52f-332">log(double)</span></span> |<span data-ttu-id="4f52f-333">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-333">double</span></span> |<span data-ttu-id="4f52f-334">double의 로그 밑 10을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-334">Returns the log base 10 of the double.</span></span> |
| <span data-ttu-id="4f52f-335">log(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-335">log(doubleVecList)</span></span> |<span data-ttu-id="4f52f-336">doubleVec</span><span class="sxs-lookup"><span data-stu-id="4f52f-336">doubleVec</span></span> |<span data-ttu-id="4f52f-337">doubleVecList의 구성 요소 로그 밑 10을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-337">Returns the component-wise log base 10 of the doubleVecList.</span></span> <span data-ttu-id="4f52f-338">vec(double)은 단일 이중 매개 변수에 대해 명시적으로 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-338">A vec(double) must be explicitly passed for the single double parameter.</span></span> <span data-ttu-id="4f52f-339">그렇지 않으면 double log(double) 버전으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-339">Otherwise, the double log(double) version is assumed.</span></span> |
| <span data-ttu-id="4f52f-340">max(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-340">max(doubleVecList)</span></span> |<span data-ttu-id="4f52f-341">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-341">double</span></span> |<span data-ttu-id="4f52f-342">doubleVecList의 최대값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-342">Returns the maximum value in the doubleVecList.</span></span> |
| <span data-ttu-id="4f52f-343">min(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-343">min(doubleVecList)</span></span> |<span data-ttu-id="4f52f-344">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-344">double</span></span> |<span data-ttu-id="4f52f-345">doubleVecList의 최소값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-345">Returns the minimum value in the doubleVecList.</span></span> |
| <span data-ttu-id="4f52f-346">norm(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-346">norm(doubleVecList)</span></span> |<span data-ttu-id="4f52f-347">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-347">double</span></span> |<span data-ttu-id="4f52f-348">doubleVecList에서 만든 벡터의 두 기준을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-348">Returns the two-norm of the vector that is created from the doubleVecList.</span></span> |
| <span data-ttu-id="4f52f-349">percentile(doubleVec v, double p)</span><span class="sxs-lookup"><span data-stu-id="4f52f-349">percentile(doubleVec v, double p)</span></span> |<span data-ttu-id="4f52f-350">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-350">double</span></span> |<span data-ttu-id="4f52f-351">벡터 v의 백분위수 요소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-351">Returns the percentile element of the vector v.</span></span> |
| <span data-ttu-id="4f52f-352">rand()</span><span class="sxs-lookup"><span data-stu-id="4f52f-352">rand()</span></span> |<span data-ttu-id="4f52f-353">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-353">double</span></span> |<span data-ttu-id="4f52f-354">0.0에서 1.0 사이의 임의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-354">Returns a random value between 0.0 and 1.0.</span></span> |
| <span data-ttu-id="4f52f-355">range(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-355">range(doubleVecList)</span></span> |<span data-ttu-id="4f52f-356">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-356">double</span></span> |<span data-ttu-id="4f52f-357">doubleVecList에 있는 최소값과 최대값 사이의 차이를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-357">Returns the difference between the min and max values in the doubleVecList.</span></span> |
| <span data-ttu-id="4f52f-358">std(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-358">std(doubleVecList)</span></span> |<span data-ttu-id="4f52f-359">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-359">double</span></span> |<span data-ttu-id="4f52f-360">doubleVecList에 있는 값의 샘플 표준 편차를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-360">Returns the sample standard deviation of the values in the doubleVecList.</span></span> |
| <span data-ttu-id="4f52f-361">stop()</span><span class="sxs-lookup"><span data-stu-id="4f52f-361">stop()</span></span> | |<span data-ttu-id="4f52f-362">자동 크기 조정 식의 평가를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-362">Stops evaluation of the autoscaling expression.</span></span> |
| <span data-ttu-id="4f52f-363">sum(doubleVecList)</span><span class="sxs-lookup"><span data-stu-id="4f52f-363">sum(doubleVecList)</span></span> |<span data-ttu-id="4f52f-364">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-364">double</span></span> |<span data-ttu-id="4f52f-365">doubleVecList에 있는 모든 구성 요소의 합계를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-365">Returns the sum of all the components of the doubleVecList.</span></span> |
| <span data-ttu-id="4f52f-366">time(string dateTime="")</span><span class="sxs-lookup"><span data-stu-id="4f52f-366">time(string dateTime="")</span></span> |<span data-ttu-id="4f52f-367">timestamp</span><span class="sxs-lookup"><span data-stu-id="4f52f-367">timestamp</span></span> |<span data-ttu-id="4f52f-368">매개 변수가 전달되지 않는 경우 현재 시간의 타임스탬프 또는 매개 변수가 전달되는 경우 dateTime 문자열의 타임스탬프를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-368">Returns the time stamp of the current time if no parameters are passed, or the time stamp of the dateTime string if it is passed.</span></span> <span data-ttu-id="4f52f-369">지원되는 dateTime 형식은 W3C-DTF 및 RFC 1123입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-369">Supported dateTime formats are W3C-DTF and RFC 1123.</span></span> |
| <span data-ttu-id="4f52f-370">val(doubleVec v, double i)</span><span class="sxs-lookup"><span data-stu-id="4f52f-370">val(doubleVec v, double i)</span></span> |<span data-ttu-id="4f52f-371">double</span><span class="sxs-lookup"><span data-stu-id="4f52f-371">double</span></span> |<span data-ttu-id="4f52f-372">시작 인덱스가 0인 벡터 v의 위치 i 요소 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-372">Returns the value of the element that is at location i in vector v, with a starting index of zero.</span></span> |

<span data-ttu-id="4f52f-373">앞의 표에서 설명하는 함수 중 일부는 목록을 인수로 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-373">Some of the functions that are described in the previous table can accept a list as an argument.</span></span> <span data-ttu-id="4f52f-374">쉼표로 구분된 목록은 *double* 및 *doubleVec*의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-374">The comma-separated list is any combination of *double* and *doubleVec*.</span></span> <span data-ttu-id="4f52f-375">예:</span><span class="sxs-lookup"><span data-stu-id="4f52f-375">For example:</span></span>

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

<span data-ttu-id="4f52f-376">*doubleVecList* 값은 평가 전 단일 *doubleVec*으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-376">The *doubleVecList* value is converted to a single *doubleVec* before evaluation.</span></span> <span data-ttu-id="4f52f-377">예를 들어 `v = [1,2,3]`의 경우 `avg(v)` 호출은 `avg(1,2,3)` 호출과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-377">For example, if `v = [1,2,3]`, then calling `avg(v)` is equivalent to calling `avg(1,2,3)`.</span></span> <span data-ttu-id="4f52f-378">`avg(v, 7)` 호출은 `avg(1,2,3,7)` 호출과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-378">Calling `avg(v, 7)` is equivalent to calling `avg(1,2,3,7)`.</span></span>

## <span data-ttu-id="4f52f-379"><a name="getsampledata"></a>샘플 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f52f-379"><a name="getsampledata"></a>Obtain sample data</span></span>
<span data-ttu-id="4f52f-380">자동 크기 조정 수식은 배치 서비스에서 제공한 메트릭 데이터(샘플)에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-380">Autoscale formulas act on metrics data (samples) that is provided by the Batch service.</span></span> <span data-ttu-id="4f52f-381">수식은 서비스에서 가져온 값에 따라 풀 크기를 늘리거나 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-381">A formula grows or shrinks pool size based on the values that it obtains from the service.</span></span> <span data-ttu-id="4f52f-382">앞에서 설명한 서비스 정의 변수는 해당 개체에 연결된 데이터에 액세스하는 다양한 메서드를 제공하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-382">The service-defined variables that were described previously are objects that provide various methods to access data that is associated with that object.</span></span> <span data-ttu-id="4f52f-383">예를 들어, 다음 식은 최근 5분 동안의 CPU 사용률을 얻기 위한 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-383">For example, the following expression shows a request to get the last five minutes of CPU usage:</span></span>

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| <span data-ttu-id="4f52f-384">메서드</span><span class="sxs-lookup"><span data-stu-id="4f52f-384">Method</span></span> | <span data-ttu-id="4f52f-385">설명</span><span class="sxs-lookup"><span data-stu-id="4f52f-385">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f52f-386">GetSample()</span><span class="sxs-lookup"><span data-stu-id="4f52f-386">GetSample()</span></span> |<span data-ttu-id="4f52f-387">`GetSample()` 메서드는 데이터 샘플의 벡터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-387">The `GetSample()` method returns a vector of data samples.</span></span><br/><br/><span data-ttu-id="4f52f-388">하나의 샘플은 30초 동안의 메트릭 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-388">A sample is 30 seconds worth of metrics data.</span></span> <span data-ttu-id="4f52f-389">즉 30초마다 샘플을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-389">In other words, samples are obtained every 30 seconds.</span></span> <span data-ttu-id="4f52f-390">그러나 아래에서 설명하듯이 샘플이 수집된 시간과 해당 샘플을 수식에 사용할 수 있게 되는 시간 사이에 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-390">But as noted below, there is a delay between when a sample is collected and when it is available to a formula.</span></span> <span data-ttu-id="4f52f-391">따라서 지정된 기간 동안 일부 샘플을 수식에 의한 평가에 사용할 수 없을지도 모릅니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-391">As such, not all samples for a given time period may be available for evaluation by a formula.</span></span><ul><li>`doubleVec GetSample(double count)`<br/><span data-ttu-id="4f52f-392">수집한 최근 샘플에서 가져올 샘플 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-392">Specifies the number of samples to obtain from the most recent samples that were collected.</span></span><br/><br/><span data-ttu-id="4f52f-393">`GetSample(1)`은 사용 가능한 마지막 샘플을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-393">`GetSample(1)` returns the last available sample.</span></span> <span data-ttu-id="4f52f-394">그러나 `$CPUPercent`와 같은 메트릭의 경우 샘플이 수집된 *시기*를 알 수 없기 때문에 이 메서드를 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-394">For metrics like `$CPUPercent`, however, this should not be used because it is impossible to know *when* the sample was collected.</span></span> <span data-ttu-id="4f52f-395">최근 샘플일 수도 있지만 시스템 문제로 인해 훨씬 오래된 샘플일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-395">It might be recent, or, because of system issues, it might be much older.</span></span> <span data-ttu-id="4f52f-396">그러한 경우 아래에 표시된 것처럼 시간 간격을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-396">It is better in such cases to use a time interval as shown below.</span></span><li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/><span data-ttu-id="4f52f-397">샘플 데이터를 수집하기 위한 시간 프레임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-397">Specifies a time frame for gathering sample data.</span></span> <span data-ttu-id="4f52f-398">선택적으로 요청 시간 프레임에 있어야 하는 샘플의 백분율을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-398">Optionally, it also specifies the percentage of samples that must be available in the requested time frame.</span></span><br/><br/><span data-ttu-id="4f52f-399">`$CPUPercent.GetSample(TimeInterval_Minute * 10)`은 지난 10분 동안의 모든 샘플이 CPUPercent 기록에 있는 경우 20개 샘플을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-399">`$CPUPercent.GetSample(TimeInterval_Minute * 10)` would return 20 samples if all samples for the last 10 minutes are present in the CPUPercent history.</span></span> <span data-ttu-id="4f52f-400">그러나 내역의 마지막 분을 사용할 수 없으면 샘플 18개만 반환될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-400">If the last minute of history was not available, however, only 18 samples would be returned.</span></span> <span data-ttu-id="4f52f-401">이 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-401">In this case:</span></span><br/><br/><span data-ttu-id="4f52f-402">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`은 샘플의 90%만 사용할 수 있으므로 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-402">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)` would fail because only 90 percent of the samples are available.</span></span><br/><br/><span data-ttu-id="4f52f-403">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)`은 성공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-403">`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` would succeed.</span></span><li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/><span data-ttu-id="4f52f-404">시작 시간과 종료 시간을 사용하여 데이터를 수집하기 위한 시간 프레임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-404">Specifies a time frame for gathering data, with both a start time and an end time.</span></span><br/><br/><span data-ttu-id="4f52f-405">위에서 언급했듯이 샘플이 수집된 시간과 해당 샘플을 수식에 사용할 수 있게 되는 시간 사이에 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-405">As mentioned above, there is a delay between when a sample is collected and when it is available to a formula.</span></span> <span data-ttu-id="4f52f-406">`GetSample` 메서드를 사용할 때 이 지연을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4f52f-406">Consider this delay when you use the `GetSample` method.</span></span> <span data-ttu-id="4f52f-407">아래 `GetSamplePercent` 참조</span><span class="sxs-lookup"><span data-stu-id="4f52f-407">See `GetSamplePercent` below.</span></span> |
| <span data-ttu-id="4f52f-408">GetSamplePeriod()</span><span class="sxs-lookup"><span data-stu-id="4f52f-408">GetSamplePeriod()</span></span> |<span data-ttu-id="4f52f-409">기록 샘플 데이터 집합에서 가져온 샘플의 기간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-409">Returns the period of samples that were taken in a historical sample data set.</span></span> |
| <span data-ttu-id="4f52f-410">Count()</span><span class="sxs-lookup"><span data-stu-id="4f52f-410">Count()</span></span> |<span data-ttu-id="4f52f-411">메트릭 기록에 있는 총 샘플 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-411">Returns the total number of samples in the metric history.</span></span> |
| <span data-ttu-id="4f52f-412">HistoryBeginTime()</span><span class="sxs-lookup"><span data-stu-id="4f52f-412">HistoryBeginTime()</span></span> |<span data-ttu-id="4f52f-413">메트릭에 대해 사용 가능한 가장 오래된 데이터 샘플의 타임스탬프를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-413">Returns the time stamp of the oldest available data sample for the metric.</span></span> |
| <span data-ttu-id="4f52f-414">GetSamplePercent()</span><span class="sxs-lookup"><span data-stu-id="4f52f-414">GetSamplePercent()</span></span> |<span data-ttu-id="4f52f-415">지정된 시간 간격에 사용할 수 있는 샘플의 백분율을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-415">Returns the percentage of samples that are available for a given time interval.</span></span> <span data-ttu-id="4f52f-416">예:</span><span class="sxs-lookup"><span data-stu-id="4f52f-416">For example:</span></span><br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/><span data-ttu-id="4f52f-417">반환된 샘플의 백분율이 지정한 `samplePercent`보다 작은 경우 `GetSample` 메서드가 실패하기 때문에 `GetSamplePercent` 메서드를 사용하여 먼저 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-417">Because the `GetSample` method fails if the percentage of samples returned is less than the `samplePercent` specified, you can use the `GetSamplePercent` method to check first.</span></span> <span data-ttu-id="4f52f-418">그런 다음 비효율적인 샘플이 존재하는 경우 자동 크기 조정 평가를 중단하지 않고 대체 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-418">Then you can perform an alternate action if insufficient samples are present, without halting the automatic scaling evaluation.</span></span> |

### <a name="samples-sample-percentage-and-the-getsample-method"></a><span data-ttu-id="4f52f-419">샘플, 샘플 비율 및 *GetSample()* 메서드</span><span class="sxs-lookup"><span data-stu-id="4f52f-419">Samples, sample percentage, and the *GetSample()* method</span></span>
<span data-ttu-id="4f52f-420">자동 크기 조정 수식의 핵심 작업은 작업 및 리소스 메트릭 데이터를 가져오고 데이터를 기반으로 풀 크기를 조정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-420">The core operation of an autoscale formula is to obtain task and resource metric data and then adjust pool size based on that data.</span></span> <span data-ttu-id="4f52f-421">따라서 자동 크기 조정 수식이 메트릭 데이터(샘플)과 상호 작용하는 방식을 명확히 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-421">As such, it is important to have a clear understanding of how autoscale formulas interact with metrics data (samples).</span></span>

<span data-ttu-id="4f52f-422">**샘플**</span><span class="sxs-lookup"><span data-stu-id="4f52f-422">**Samples**</span></span>

<span data-ttu-id="4f52f-423">Batch 서비스는 정기적으로 작업 및 리소스 메트릭의 샘플을 가져와 자동 크기 조정 수식에 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-423">The Batch service periodically takes samples of task and resource metrics and makes them available to your autoscale formulas.</span></span> <span data-ttu-id="4f52f-424">이러한 샘플은 배치 서비스에서 30초 마다 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-424">These samples are recorded every 30 seconds by the Batch service.</span></span> <span data-ttu-id="4f52f-425">하지만 일반적으로 이러한 샘플을 기록하는 시간과 자동 크기 조정 수식에서 사용할 수 있을 시간(읽을 수 있는 시간) 사이에 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-425">However, there is typically a delay between when those samples were recorded and when they are made available to (and can be read by) your autoscale formulas.</span></span> <span data-ttu-id="4f52f-426">또한 네트워크 또는 다른 인프라 문제와 같이 다양한 요인으로 인해 샘플이 특정 기간에 기록되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-426">Additionally, due to various factors such as network or other infrastructure issues, samples may not be recorded for a particular interval.</span></span>

<span data-ttu-id="4f52f-427">**샘플 비율**</span><span class="sxs-lookup"><span data-stu-id="4f52f-427">**Sample percentage**</span></span>

<span data-ttu-id="4f52f-428">`samplePercent`를 `GetSample()` 메서드에 전달하거나 `GetSamplePercent()` 메서드를 호출하는 경우 _percent_(비율)는 Batch 서비스에서 기록하는 샘플의 가능한 총 수와 자동 크기 조정 수식에서 사용할 수 있는 샘플 수를 비교한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-428">When `samplePercent` is passed to the `GetSample()` method or the `GetSamplePercent()` method is called, _percent_ refers to a comparison between the total possible number of samples that are recorded by the Batch service and the number of samples that are available to your autoscale formula.</span></span>

<span data-ttu-id="4f52f-429">예를 들어 10분 TimeSpan을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-429">Let's look at a 10-minute timespan as an example.</span></span> <span data-ttu-id="4f52f-430">샘플이 10분 시간 간격 내에서 30초마다 기록되므로 Batch에 서 기록하는 샘플의 최대 총 수는 20개 샘플(분당 2개)입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-430">Because samples are recorded every 30 seconds within a 10-minute timespan, the maximum total number of samples that are recorded by Batch would be 20 samples (2 per minute).</span></span> <span data-ttu-id="4f52f-431">그러나 보고 메커니즘의 고유한 대기 시간 또는 Azure 내의 다른 문제로 인해 자동 크기 조정 수식에서 읽는 데 사용할 수 있는 샘플은 15개뿐일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-431">However, due to the inherent latency of the reporting mechanism and other issues within Azure, there may be only 15 samples that are available to your autoscale formula for reading.</span></span> <span data-ttu-id="4f52f-432">즉 10분 동안 기록하는 샘플의 총 개수 중 75%만 수식에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-432">So, for example, for that 10-minute period, only 75% of the total number of samples recorded may be available to your formula.</span></span>

<span data-ttu-id="4f52f-433">**GetSample() 및 샘플 범위**</span><span class="sxs-lookup"><span data-stu-id="4f52f-433">**GetSample() and sample ranges**</span></span>

<span data-ttu-id="4f52f-434">자동 크기 조정 수식은 풀을 확장하거나 축소합니다. 즉 노드를 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-434">Your autoscale formulas are going to be growing and shrinking your pools &mdash; adding nodes or removing nodes.</span></span> <span data-ttu-id="4f52f-435">노드에 비용이 들기 때문에 수식은 충분한 데이터를 기반으로 지능형 분석 메서드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-435">Because nodes cost you money, you want to ensure that your formulas use an intelligent method of analysis that is based on sufficient data.</span></span> <span data-ttu-id="4f52f-436">따라서 수식에서 추세 형식 분석을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-436">Therefore, we recommend that you use a trending-type analysis in your formulas.</span></span> <span data-ttu-id="4f52f-437">이 형식은 수집된 샘플의 범위에 따라 풀을 확장하고 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-437">This type grows and shrinks your pools based on a range of collected samples.</span></span>

<span data-ttu-id="4f52f-438">이렇게 하려면 `GetSample(interval look-back start, interval look-back end)`를 사용하여 샘플의 벡터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-438">To do so, use `GetSample(interval look-back start, interval look-back end)` to return a vector of samples:</span></span>

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

<span data-ttu-id="4f52f-439">위의 줄이 Batch에 의해 확인된 경우 다양한 샘플을 값의 벡터로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-439">When the above line is evaluated by Batch, it returns a range of samples as a vector of values.</span></span> <span data-ttu-id="4f52f-440">예:</span><span class="sxs-lookup"><span data-stu-id="4f52f-440">For example:</span></span>

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

<span data-ttu-id="4f52f-441">샘플의 벡터를 수집했으면 `min()`, `max()` 및 `avg()`과 같은 함수를 사용하여 수집된 범위에서 의미 있는 값을 파생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-441">Once you've collected the vector of samples, you can then use functions like `min()`, `max()`, and `avg()` to derive meaningful values from the collected range.</span></span>

<span data-ttu-id="4f52f-442">추가 보안을 위해 특정 샘플 비율 미만을 특정 기간 동안 사용할 수 있는 경우 수식 평가가 실패하도록 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-442">For additional security, you can force a formula evaluation to fail if less than a certain sample percentage is available for a particular time period.</span></span> <span data-ttu-id="4f52f-443">수식 평가가 실패하도록 강제하면 지정된 샘플 비율을 사용할 수 없는 경우 Batch에 수식의 추가 평가를 중단하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-443">When you force a formula evaluation to fail, you instruct Batch to cease further evaluation of the formula if the specified percentage of samples is not available.</span></span> <span data-ttu-id="4f52f-444">이 경우 풀 크기가 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-444">In this case, no change is made to the pool size.</span></span> <span data-ttu-id="4f52f-445">평가가 성공하기 위해 샘플의 필요한 백분율을 지정하려면 `GetSample()`에 대한 세 번째 매개 변수로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-445">To specify a required percentage of samples for the evaluation to succeed, specify it as the third parameter to `GetSample()`.</span></span> <span data-ttu-id="4f52f-446">여기에서는 샘플의 75% 요구 사항이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-446">Here, a requirement of 75 percent of samples is specified:</span></span>

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

<span data-ttu-id="4f52f-447">또한 샘플 가용성에 지연 시간이 있을 수 있으므로 시간 범위를 1분 이상인 돌아보기 시작 시간으로 지정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-447">Because there may be a delay in sample availability, it is important to always specify a time range with a look-back start time that is older than one minute.</span></span> <span data-ttu-id="4f52f-448">샘플이 시스템을 통해 전파되는 데 약 1분 정도가 걸리므로 `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` 범위에 있는 샘플은 사용하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-448">It takes approximately one minute for samples to propagate through the system, so samples in the range `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` may not be available.</span></span> <span data-ttu-id="4f52f-449">다시 `GetSample()`라는 백분율 매개 변수를 사용하여 특정 샘플 비율 요구 사항을 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-449">Again, you can use the percentage parameter of `GetSample()` to force a particular sample percentage requirement.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f52f-450">**자동 크기 조정 수식의 `GetSample(1)`*만* 신뢰하지 않는** 것이 **좋습니다**.</span><span class="sxs-lookup"><span data-stu-id="4f52f-450">We **strongly recommend** that you **avoid relying *only* on `GetSample(1)` in your autoscale formulas**.</span></span> <span data-ttu-id="4f52f-451">`GetSample(1)`은 기본적으로 Batch 서비스에 “경과한 시간에 관계 없이 마지막 샘플을 제공하도록” 요구하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-451">This is because `GetSample(1)` essentially says to the Batch service, "Give me the last sample you have, no matter how long ago you retrieved it."</span></span> <span data-ttu-id="4f52f-452">이 샘플은 단일 샘플이고 오래된 샘플이기 때문에 최근 작업 또는 리소스 상태의 큰 그림을 나타내지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-452">Since it is only a single sample, and it may be an older sample, it may not be representative of the larger picture of recent task or resource state.</span></span> <span data-ttu-id="4f52f-453">`GetSample(1)`을 사용하는 경우 큰 문의 일부이며 수식이 사용하는 유일한 데이터 지점이 아니도록 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-453">If you do use `GetSample(1)`, make sure that it's part of a larger statement and not the only data point that your formula relies on.</span></span>
>
>

## <a name="metrics"></a><span data-ttu-id="4f52f-454">메트릭</span><span class="sxs-lookup"><span data-stu-id="4f52f-454">Metrics</span></span>
<span data-ttu-id="4f52f-455">수식을 정의할 때 리소스 및 작업 메트릭을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-455">You can use both resource and task metrics when you're defining a formula.</span></span> <span data-ttu-id="4f52f-456">가져오고 평가한 메트릭 데이터를 기반으로 하는 풀의 전용 노드 대상 수를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-456">You adjust the target number of dedicated nodes in the pool based on the metrics data that you obtain and evaluate.</span></span> <span data-ttu-id="4f52f-457">각 메트릭에 대한 자세한 내용은 위의 [변수](#variables) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f52f-457">See the [Variables](#variables) section above for more information on each metric.</span></span>

<table>
  <tr>
    <th><span data-ttu-id="4f52f-458">메트릭</span><span class="sxs-lookup"><span data-stu-id="4f52f-458">Metric</span></span></th>
    <th><span data-ttu-id="4f52f-459">설명</span><span class="sxs-lookup"><span data-stu-id="4f52f-459">Description</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="4f52f-460"><b>리소스</b></span><span class="sxs-lookup"><span data-stu-id="4f52f-460"><b>Resource</b></span></span></td>
    <td><p><span data-ttu-id="4f52f-461">리소스 메트릭은 CPU, 대역폭, 계산 노드의 메모리 사용량 및 노드 수를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-461">Resource metrics are based on the CPU, the bandwidth, the memory usage of compute nodes, and the number of nodes.</span></span></p>
        <p> <span data-ttu-id="4f52f-462">이러한 서비스 정의 변수는 노드 수에 기반하여 조정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-462">These service-defined variables are useful for making adjustments based on node count:</span></span></p>
    <p><ul>
            <li><span data-ttu-id="4f52f-463">$TargetDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="4f52f-463">$TargetDedicatedNodes</span></span></li>
            <li><span data-ttu-id="4f52f-464">$TargetLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="4f52f-464">$TargetLowPriorityNodes</span></span></li>
            <li><span data-ttu-id="4f52f-465">$CurrentDedicatedNodes</span><span class="sxs-lookup"><span data-stu-id="4f52f-465">$CurrentDedicatedNodes</span></span></li>
            <li><span data-ttu-id="4f52f-466">$CurrentLowPriorityNodes</span><span class="sxs-lookup"><span data-stu-id="4f52f-466">$CurrentLowPriorityNodes</span></span></li>
            <li><span data-ttu-id="4f52f-467">$preemptedNodeCount</span><span class="sxs-lookup"><span data-stu-id="4f52f-467">$preemptedNodeCount</span></span></li>
            <li><span data-ttu-id="4f52f-468">$SampleNodeCount</span><span class="sxs-lookup"><span data-stu-id="4f52f-468">$SampleNodeCount</span></span></li>
    </ul></p>
    <p><span data-ttu-id="4f52f-469">이러한 서비스 정의 변수는 노드 리소스 사용량에 기반하여 조정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-469">These service-defined variables are useful for making adjustments based on node resource usage:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="4f52f-470">$CPUPercent</span><span class="sxs-lookup"><span data-stu-id="4f52f-470">$CPUPercent</span></span></li>
      <li><span data-ttu-id="4f52f-471">$WallClockSeconds</span><span class="sxs-lookup"><span data-stu-id="4f52f-471">$WallClockSeconds</span></span></li>
      <li><span data-ttu-id="4f52f-472">$MemoryBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-472">$MemoryBytes</span></span></li>
      <li><span data-ttu-id="4f52f-473">$DiskBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-473">$DiskBytes</span></span></li>
      <li><span data-ttu-id="4f52f-474">$DiskReadBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-474">$DiskReadBytes</span></span></li>
      <li><span data-ttu-id="4f52f-475">$DiskWriteBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-475">$DiskWriteBytes</span></span></li>
      <li><span data-ttu-id="4f52f-476">$DiskReadOps</span><span class="sxs-lookup"><span data-stu-id="4f52f-476">$DiskReadOps</span></span></li>
      <li><span data-ttu-id="4f52f-477">$DiskWriteOps</span><span class="sxs-lookup"><span data-stu-id="4f52f-477">$DiskWriteOps</span></span></li>
      <li><span data-ttu-id="4f52f-478">$NetworkInBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-478">$NetworkInBytes</span></span></li>
      <li><span data-ttu-id="4f52f-479">$NetworkOutBytes</span><span class="sxs-lookup"><span data-stu-id="4f52f-479">$NetworkOutBytes</span></span></li></ul></p>
  </tr>
  <tr>
    <td><span data-ttu-id="4f52f-480"><b>작업</b></span><span class="sxs-lookup"><span data-stu-id="4f52f-480"><b>Task</b></span></span></td>
    <td><p><span data-ttu-id="4f52f-481">작업 메트릭은 활성, 보류 중 및 완료됨과 같은 작업 상태를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-481">Task metrics are based on the status of tasks, such as Active, Pending, and Completed.</span></span> <span data-ttu-id="4f52f-482">다음 서비스 정의 변수는 노드 작업 메트릭에 기반하여 풀 크기를 조정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-482">The following service-defined variables are useful for making pool-size adjustments based on task metrics:</span></span></p>
    <p><ul>
      <li><span data-ttu-id="4f52f-483">$ActiveTasks</span><span class="sxs-lookup"><span data-stu-id="4f52f-483">$ActiveTasks</span></span></li>
      <li><span data-ttu-id="4f52f-484">$RunningTasks</span><span class="sxs-lookup"><span data-stu-id="4f52f-484">$RunningTasks</span></span></li>
      <li><span data-ttu-id="4f52f-485">$PendingTasks</span><span class="sxs-lookup"><span data-stu-id="4f52f-485">$PendingTasks</span></span></li>
      <li><span data-ttu-id="4f52f-486">$SucceededTasks</span><span class="sxs-lookup"><span data-stu-id="4f52f-486">$SucceededTasks</span></span></li>
            <li><span data-ttu-id="4f52f-487">$FailedTasks</span><span class="sxs-lookup"><span data-stu-id="4f52f-487">$FailedTasks</span></span></li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a><span data-ttu-id="4f52f-488">자동 크기 조정 수식 작성</span><span class="sxs-lookup"><span data-stu-id="4f52f-488">Write an autoscale formula</span></span>
<span data-ttu-id="4f52f-489">위의 구성 요소를 사용하는 구문을 구성하여 자동 크기 조정 수식을 작성한 다음 해당 구문을 완전한 수식으로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-489">You build an autoscale formula by forming statements that use the above components, then combine those statements into a complete formula.</span></span> <span data-ttu-id="4f52f-490">이 섹션에서는 몇 가지 실제 크기 조정을 결정할 수 있는 자동 크기 조정 수식 예제를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-490">In this section, we create an example autoscale formula that can perform some real-world scaling decisions.</span></span>

<span data-ttu-id="4f52f-491">먼저 새 자동 크기 조정 수식에 대한 요구 사항을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-491">First, let's define the requirements for our new autoscale formula.</span></span> <span data-ttu-id="4f52f-492">수식은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-492">The formula should:</span></span>

1. <span data-ttu-id="4f52f-493">CPU 사용량이 많은 경우 풀에 있는 전용 계산 노드의 목표 수를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-493">Increase the target number of dedicated compute nodes in a pool if CPU usage is high.</span></span>
2. <span data-ttu-id="4f52f-494">CPU 사용량이 적은 경우 풀에 있는 전용 계산 노드의 목표 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-494">Decrease the target number of dedicated compute nodes in a pool when CPU usage is low.</span></span>
3. <span data-ttu-id="4f52f-495">전용 노드의 최대 수는 항상 400으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-495">Always restrict the maximum number of dedicated nodes to 400.</span></span>

<span data-ttu-id="4f52f-496">CPU 사용량이 많은 동안 노드 수를 늘리려면, 지난 10분 동안 CPU 최소 평균 사용량이 70%를 초과한 경우에만 사용자 정의 변수(`$totalDedicatedNodes`)를 전용 노드의 현재 목표 수의 110%인 값으로 채우는 문을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-496">To increase the number of nodes during high CPU usage, define the statement that populates a user-defined variable (`$totalDedicatedNodes`) with a value that is 110 percent of the current target number of dedicated nodes, but only if the minimum average CPU usage during the last 10 minutes was above 70 percent.</span></span> <span data-ttu-id="4f52f-497">그렇지 않으면 전용 노드의 현재 수에 대한 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-497">Otherwise, use the value for the current number of dedicated nodes.</span></span>

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

<span data-ttu-id="4f52f-498">CPU 사용량이 많은 동안 노드 수를 *줄이려면*, 지난 60분 동안 CPU 평균 사용량이 20% 미만인 경우 수식의 다음 문에서 동일한 `$totalDedicatedNodes` 변수를 전용 노드의 현재 목표 수의 90%로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-498">To *decrease* the number of dedicated nodes during low CPU usage, the next statement in our formula sets the same `$totalDedicatedNodes` variable to 90 percent of the current target number of dedicated nodes if the average CPU usage in the past 60 minutes was under 20 percent.</span></span> <span data-ttu-id="4f52f-499">그렇지 않으면 위 구문에 채워진 `$totalDedicatedNodes`의 현재 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-499">Otherwise, use the current value of `$totalDedicatedNodes` that we populated in the statement above.</span></span>

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

<span data-ttu-id="4f52f-500">이제 전용 계산 노드의 목표 수를 최대 400으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-500">Now limit the target number of dedicated compute nodes to a maximum of 400:</span></span>

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

<span data-ttu-id="4f52f-501">완성된 수식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-501">Here's the complete formula:</span></span>

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a><span data-ttu-id="4f52f-502">.NET으로 자동 크기 조정 가능한 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="4f52f-502">Create an autoscale-enabled pool with .NET</span></span>

<span data-ttu-id="4f52f-503">.NET에서 자동 크기 조정 가능한 풀을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-503">To create a pool with autoscaling enabled in .NET, follow these steps:</span></span>

1. <span data-ttu-id="4f52f-504">[BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool)을 사용하여 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-504">Create the pool with [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).</span></span>
2. <span data-ttu-id="4f52f-505">[CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) 속성을 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-505">Set the [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) property to `true`.</span></span>
3. <span data-ttu-id="4f52f-506">자동 크기 조정 수식을 사용하여 [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-506">Set the [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) property with your autoscale formula.</span></span>
4. <span data-ttu-id="4f52f-507">(선택 사항) [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) 속성을 설정합니다(기본값: 15 분).</span><span class="sxs-lookup"><span data-stu-id="4f52f-507">(Optional) Set the [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) property (default is 15 minutes).</span></span>
5. <span data-ttu-id="4f52f-508">[CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) 또는 [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync)로 풀을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-508">Commit the pool with [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) or [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).</span></span>

<span data-ttu-id="4f52f-509">다음 코드 조각에서는 .NET에서 자동 크기 조정 가능한 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-509">The following code snippet creates an autoscale-enabled pool in .NET.</span></span> <span data-ttu-id="4f52f-510">풀의 자동 크기 조정 수식에서 전용 노드의 목표 수를 월요일에는 5로, 그 외 다른 요일에는 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-510">The pool's autoscale formula sets the target number of dedicated nodes to 5 on Mondays, and 1 on every other day of the week.</span></span> <span data-ttu-id="4f52f-511">[자동 크기 조정 간격](#automatic-scaling-interval)은 30분으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-511">The [automatic scaling interval](#automatic-scaling-interval) is set to 30 minutes.</span></span> <span data-ttu-id="4f52f-512">이 코드 조각과 이 문서의 다른 C# 코드 조각에서 `myBatchClient`는 [BatchClient][net_batchclient] 클래스의 올바르게 초기화된 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-512">In this and the other C# snippets in this article, `myBatchClient` is a properly initialized instance of the [BatchClient][net_batchclient] class.</span></span>

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
> <span data-ttu-id="4f52f-513">자동 크기 조정 가능한 풀을 만들 때는 **CreatePool**에 대한 호출에서 _targetDedicatedComputeNodes_ 매개 변수 또는 _targetLowPriorityComputeNodes_ 매개 변수를 지정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4f52f-513">When you create an autoscale-enabled pool, do not specify the _targetDedicatedComputeNodes_ parameter or the _targetLowPriorityComputeNodes_ parameter on the call to **CreatePool**.</span></span> <span data-ttu-id="4f52f-514">대신 풀에 **AutoScaleEnabled** 및 **AutoScaleFormula** 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-514">Instead, specify the **AutoScaleEnabled** and **AutoScaleFormula** properties on the pool.</span></span> <span data-ttu-id="4f52f-515">이러한 속성의 값은 각 노드 형식의 목표 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-515">The values for these properties determine the target number of each type of node.</span></span> <span data-ttu-id="4f52f-516">또한 자동 크기 조정 가능한 풀의 크기를 수동으로 조정하려는 경우(예: [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync] 사용) 먼저 풀에서 자동 크기 조정을 **사용하지 않도록** 설정한 다음 풀의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-516">Also, to manually resize an autoscale-enabled pool (for example, with [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), first **disable** automatic scaling on the pool, then resize it.</span></span>
>
>

<span data-ttu-id="4f52f-517">Batch .NET 외에도 다른 [Batch SDK](batch-apis-tools.md#azure-accounts-for-batch-development), [Batch REST](https://docs.microsoft.com/rest/api/batchservice/), [Batch PowerShell cmdlet](batch-powershell-cmdlets-get-started.md) 및 [Batch CLI](batch-cli-get-started.md) 중 하나를 사용하여 자동 크기 조정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-517">In addition to Batch .NET, you can use any of the other [Batch SDKs](batch-apis-tools.md#azure-accounts-for-batch-development), [Batch REST](https://docs.microsoft.com/rest/api/batchservice/), [Batch PowerShell cmdlets](batch-powershell-cmdlets-get-started.md), and the [Batch CLI](batch-cli-get-started.md) to configure autoscaling.</span></span>


### <a name="automatic-scaling-interval"></a><span data-ttu-id="4f52f-518">자동 크기 조정 간격</span><span class="sxs-lookup"><span data-stu-id="4f52f-518">Automatic scaling interval</span></span>
<span data-ttu-id="4f52f-519">기본적으로 Batch 서비스는 15분마다 자동 크기 조정 수식에 따라 풀의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-519">By default, the Batch service adjusts a pool's size according to its autoscale formula every 15 minutes.</span></span> <span data-ttu-id="4f52f-520">이 간격은 다음 풀 속성을 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-520">This interval is configurable by using the following pool properties:</span></span>

* <span data-ttu-id="4f52f-521">[CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)</span><span class="sxs-lookup"><span data-stu-id="4f52f-521">[CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)</span></span>
* <span data-ttu-id="4f52f-522">[autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)</span><span class="sxs-lookup"><span data-stu-id="4f52f-522">[autoScaleEvaluationInterval][rest_autoscaleinterval] (REST API)</span></span>

<span data-ttu-id="4f52f-523">최소 간격은 5분이고 최대 간격은 168시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-523">The minimum interval is five minutes, and the maximum is 168 hours.</span></span> <span data-ttu-id="4f52f-524">이 범위를 벗어나는 간격을 지정하면 Batch 서비스에서 잘못된 요청(400) 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-524">If an interval outside this range is specified, the Batch service returns a Bad Request (400) error.</span></span>

> [!NOTE]
> <span data-ttu-id="4f52f-525">자동 크기 조정은 현재 1분 미만의 변경 내용에 응답하지 않지만 워크로드를 실행하면 점차적으로 풀의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-525">Autoscaling is not currently intended to respond to changes in less than a minute, but rather is intended to adjust the size of your pool gradually as you run a workload.</span></span>
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a><span data-ttu-id="4f52f-526">기존 풀에서 자동 크기 조정 사용</span><span class="sxs-lookup"><span data-stu-id="4f52f-526">Enable autoscaling on an existing pool</span></span>

<span data-ttu-id="4f52f-527">Batch SDK마다 자동 크기 조정을 사용하도록 설정하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-527">Each Batch SDK provides a way to enable autoscaling.</span></span> <span data-ttu-id="4f52f-528">예:</span><span class="sxs-lookup"><span data-stu-id="4f52f-528">For example:</span></span>

* <span data-ttu-id="4f52f-529">[BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync](Batch .NET)</span><span class="sxs-lookup"><span data-stu-id="4f52f-529">[BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (Batch .NET)</span></span>
* <span data-ttu-id="4f52f-530">[풀에서 자동 크기 조정 사용][rest_enableautoscale] (REST API)</span><span class="sxs-lookup"><span data-stu-id="4f52f-530">[Enable automatic scaling on a pool][rest_enableautoscale] (REST API)</span></span>

<span data-ttu-id="4f52f-531">기존 풀에서 자동 크기 조정을 사용하도록 설정하는 경우 다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="4f52f-531">When you enable autoscaling on an existing pool, keep in mind the following points:</span></span>

* <span data-ttu-id="4f52f-532">자동 크기 조정을 사용하기 위한 요청을 발급할 때 현재 풀에서 자동 크기 조정을 사용하지 않도록 설정되어 있으면 이 요청을 발급할 때 유효한 자동 크기 조정 수식을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-532">If automatic scaling is currently disabled on the pool when you issue the request to enable autoscaling, you must specify a valid autoscale formula when you issue the request.</span></span> <span data-ttu-id="4f52f-533">필요에 따라 자동 크기 조정 평가 간격을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-533">You can optionally specify an autoscale evaluation interval.</span></span> <span data-ttu-id="4f52f-534">간격을 지정하지 않으면 기본값인 15분이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-534">If you do not specify an interval, the default value of 15 minutes is used.</span></span>
* <span data-ttu-id="4f52f-535">현재 풀에서 자동 크기 조정을 사용할 수 있는 경우 자동 크기 조정 수식, 평가 간격 또는 둘 다를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-535">If autoscale is currently enabled on the pool, you can specify an autoscale formula, an evaluation interval, or both.</span></span> <span data-ttu-id="4f52f-536">이러한 속성 중 하나 이상을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-536">You must specify at least one of these properties.</span></span>

  * <span data-ttu-id="4f52f-537">새로운 자동 크기 조정 간격을 지정하면 기존 평가 일정이 중지되고 새 일정이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-537">If you specify a new autoscale evaluation interval, then the existing evaluation schedule is stopped and a new schedule is started.</span></span> <span data-ttu-id="4f52f-538">새 일정의 시작 시간은 자동 크기 조정을 사용하기 위한 요청이 발급된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-538">The new schedule's start time is the time at which the request to enable autoscaling was issued.</span></span>
  * <span data-ttu-id="4f52f-539">자동 크기 조정 수식 또는 평가 간격을 생략하면 배치 서비스에서 해당 설정의 현재 값을 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-539">If you omit either the autoscale formula or evaluation interval, the Batch service continues to use the current value of that setting.</span></span>

> [!NOTE]
> <span data-ttu-id="4f52f-540">.NET에서 풀을 만들 때 **CreatePool** 메서드의 *targetDedicatedComputeNodes* 또는 *targetLowPriorityComputeNodes* 매개 변수에 대한 값을 지정했거나 다른 언어의 비교 가능한 매개 변수에 대한 값을 지정한 경우, 자동 크기 조정 수식을 평가할 때 해당 값이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-540">If you specified values for the *targetDedicatedComputeNodes* or *targetLowPriorityComputeNodes* parameters of the **CreatePool** method when you created the pool in .NET, or for the comparable parameters in another language, then those values are ignored when the automatic scaling formula is evaluated.</span></span>
>
>

<span data-ttu-id="4f52f-541">이 C# 코드 조각에서 다음과 같이 [Batch .NET][net_api] 라이브러리를 사용하여 기존 풀에서 자동 크기 조정을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-541">This C# code snippet uses the [Batch .NET][net_api] library to enable autoscaling on an existing pool:</span></span>

```csharp
// Define the autoscaling formula. This formula sets the target number of nodes
// to 5 on Mondays, and 1 on every other day of the week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set the autoscale formula on the existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a><span data-ttu-id="4f52f-542">자동 크기 조정 수식 업데이트</span><span class="sxs-lookup"><span data-stu-id="4f52f-542">Update an autoscale formula</span></span>

<span data-ttu-id="4f52f-543">기존의 자동 크기 조정 가능한 풀에서 수식을 업데이트하려면 새 수식을 사용하여 자동 크기 조정을 사용하도록 다시 설정하는 작업을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-543">To update the formula on an existing autoscale-enabled pool, call the operation to enable autoscaling again with the new formula.</span></span> <span data-ttu-id="4f52f-544">예를 들어 다음 .NET 코드가 실행될 때 `myexistingpool`에서 자동 크기 조정을 사용하도록 이미 설정되어 있으면 자동 크기 조정 수식이 `myNewFormula`의 내용으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-544">For example, if autoscaling is already enabled on `myexistingpool` when the following .NET code is executed, its autoscale formula is replaced with the contents of `myNewFormula`.</span></span>

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-the-autoscale-interval"></a><span data-ttu-id="4f52f-545">자동 크기 조정 간격 업데이트</span><span class="sxs-lookup"><span data-stu-id="4f52f-545">Update the autoscale interval</span></span>

<span data-ttu-id="4f52f-546">기존의 자동 크기 조정 가능한 풀의 자동 크기 조정 평가 간격을 업데이트하려면 새 간격으로 자동 크기 조정을 사용하도록 다시 설정하는 작업을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-546">To update the autoscale evaluation interval of an existing autoscale-enabled pool, call the operation to enable autoscaling again with the new interval.</span></span> <span data-ttu-id="4f52f-547">예를 들어 .NET에서 이미 자동 크기 조정 가능한 풀에 대해 자동 크기 조정 평가 간격을 60분으로 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-547">For example, to set the autoscale evaluation interval to 60 minutes for a pool that's already autoscale-enabled in .NET:</span></span>

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a><span data-ttu-id="4f52f-548">자동 크기 조정 수식 평가</span><span class="sxs-lookup"><span data-stu-id="4f52f-548">Evaluate an autoscale formula</span></span>

<span data-ttu-id="4f52f-549">수식은 풀에 적용하기 전에 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-549">You can evaluate a formula before applying it to a pool.</span></span> <span data-ttu-id="4f52f-550">이러한 방법으로 수식을 테스트하여 프로덕션 환경에 해당 수식을 배포하기 전에 문이 평가되는 방식을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-550">In this way, you can test the formula to see how its statements evaluate before you put the formula into production.</span></span>

<span data-ttu-id="4f52f-551">자동 크기 조정 수식을 평가하려면 먼저 유효한 수식을 사용하여 풀에서 자동 크기 조정을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-551">To evaluate an autoscale formula, you must first enable autoscaling on the pool with a valid formula.</span></span> <span data-ttu-id="4f52f-552">아직 자동 크기 조정을 사용할 수 없는 풀에서 수식을 테스트하려면 자동 크기 조정을 처음 사용할 때 한 줄로 구성된 `$TargetDedicatedNodes = 0` 수식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-552">To test a formula on a pool that doesn't yet have autoscaling enabled, use the one-line formula `$TargetDedicatedNodes = 0` when you first enable autoscaling.</span></span> <span data-ttu-id="4f52f-553">그런 후에 다음 중 하나를 사용하여 테스트할 수식을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-553">Then, use one of the following to evaluate the formula you want to test:</span></span>

* <span data-ttu-id="4f52f-554">[BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) 또는 [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)</span><span class="sxs-lookup"><span data-stu-id="4f52f-554">[BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) or [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)</span></span>

    <span data-ttu-id="4f52f-555">이러한 배치.NET 메서드를 사용하려면 기존 풀의 ID와 평가할 자동 크기 조정 수식이 포함된 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-555">These Batch .NET methods require the ID of an existing pool and a string containing the autoscale formula to evaluate.</span></span>

* [<span data-ttu-id="4f52f-556">자동 크기 조정 수식 평가</span><span class="sxs-lookup"><span data-stu-id="4f52f-556">Evaluate an automatic scaling formula</span></span>](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    <span data-ttu-id="4f52f-557">이 REST API 요청에서 풀 ID는 URI에 지정하고, 자동 크기 조정 수식은 요청 본문의 *autoScaleFormula* 요소에 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-557">In this REST API request, specify the pool ID in the URI, and the autoscale formula in the *autoScaleFormula* element of the request body.</span></span> <span data-ttu-id="4f52f-558">작업 응답에는 수식과 관련이 있을 수 있는 오류 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-558">The response of the operation contains any error information that might be related to the formula.</span></span>

<span data-ttu-id="4f52f-559">이 [Batch .NET][net_api] 코드 조각에서는 자동 크기 조정 수식을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-559">In this [Batch .NET][net_api] code snippet, we evaluate an autoscale formula.</span></span> <span data-ttu-id="4f52f-560">풀에서 자동 크기 조정을 사용할 수 없으면 먼저 풀에서 이 기능을 사용할 수 있도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-560">If the pool does not have autoscaling enabled, we enable it first.</span></span>

```csharp
// First obtain a reference to an existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on the pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula to enable autoscaling on the
    // pool. This formula is valid, but won't resize the pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls to once every 30 seconds.
    // Because we want to apply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here to ensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh the properties of the pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on the pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // The formula to evaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform the autoscale formula evaluation. Note that this code does not
    // actually apply the formula to the pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print the results of the AutoScaleRun.
        // This will display the values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply the formula to the pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output the message associated with the error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

<span data-ttu-id="4f52f-561">이 코드 조각에 표시된 수식을 성공적으로 평가하면 다음과 비슷한 결과가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-561">Successful evaluation of the formula shown in this code snippet produces results similar to:</span></span>

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a><span data-ttu-id="4f52f-562">자동 크기 조정 실행에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f52f-562">Get information about autoscale runs</span></span>

<span data-ttu-id="4f52f-563">수식이 예상대로 수행되는지 확인하려면 풀에서 자동 크기 조정을 실행한 결과를 Batch에서 정기적으로 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-563">To ensure that your formula is performing as expected, we recommend that you periodically check the results of the autoscaling runs that Batch performs on your pool.</span></span> <span data-ttu-id="4f52f-564">이렇게 하려면 풀에 대한 참조를 가져오고(또는 새로 고침) 마지막 자동 크기 조정 실행의 속성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-564">To do so, get (or refresh) a reference to the pool, and examine the properties of its last autoscale run.</span></span>

<span data-ttu-id="4f52f-565">Batch .NET에서 [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) 속성에는 풀에서 수행된 마지막 자동 크기 조정 실행에 대한 정보를 제공하는 몇 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-565">In Batch .NET, the [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) property has several properties that provide information about the latest automatic scaling run performed on the pool:</span></span>

* [<span data-ttu-id="4f52f-566">AutoScaleRun.Timestamp</span><span class="sxs-lookup"><span data-stu-id="4f52f-566">AutoScaleRun.Timestamp</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [<span data-ttu-id="4f52f-567">AutoScaleRun.Results</span><span class="sxs-lookup"><span data-stu-id="4f52f-567">AutoScaleRun.Results</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [<span data-ttu-id="4f52f-568">AutoScaleRun.Error</span><span class="sxs-lookup"><span data-stu-id="4f52f-568">AutoScaleRun.Error</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

<span data-ttu-id="4f52f-569">REST API에서 [풀에 대한 정보 가져오기](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) 요청은 [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) 속성에 마지막 자동 크기 조정 실행 정보가 포함된 풀 관련 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-569">In the REST API, the [Get information about a pool](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) request returns information about the pool, which includes the latest automatic scaling run information in the [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) property.</span></span>

<span data-ttu-id="4f52f-570">다음 C# 코드 조각에서는 Batch .NET 라이브러리를 사용하여 _myPool_ 풀에서 마지막으로 실행된 자동 크기 조정에 대한 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-570">The following C# code snippet uses the Batch .NET library to print information about the last autoscaling run on pool _myPool_:</span></span>

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

<span data-ttu-id="4f52f-571">앞에서 언급한 코드 조각의 샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-571">Sample output of the preceding snippet:</span></span>

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

## <a name="example-autoscale-formulas"></a><span data-ttu-id="4f52f-572">자동 크기 조정 수식 예제</span><span class="sxs-lookup"><span data-stu-id="4f52f-572">Example autoscale formulas</span></span>
<span data-ttu-id="4f52f-573">풀의 계산 리소스 양을 조정하는 여러 가지 방법을 보여 주는 몇 가지 수식을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-573">Let's look at a few formulas that show different ways to adjust the amount of compute resources in a pool.</span></span>

### <a name="example-1-time-based-adjustment"></a><span data-ttu-id="4f52f-574">예제1: 시간 기반 조정</span><span class="sxs-lookup"><span data-stu-id="4f52f-574">Example 1: Time-based adjustment</span></span>
<span data-ttu-id="4f52f-575">요일과 시간에 따라 풀 크기를 조정한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-575">Suppose you want to adjust the pool size based on the day of the week and time of day.</span></span> <span data-ttu-id="4f52f-576">이 예제에서는 풀의 노드 수를 적절히 늘리거나 줄이는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-576">This example shows how to increase or decrease the number of nodes in the pool accordingly.</span></span>

<span data-ttu-id="4f52f-577">먼저 수식에서 현재 시간을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-577">The formula first obtains the current time.</span></span> <span data-ttu-id="4f52f-578">평일(1-5)에 근무 시간(오전 8시-오후 6시)인 경우, 대상 풀 크기는 20개의 노드로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-578">If it's a weekday (1-5) and within working hours (8 AM to 6 PM), the target pool size is set to 20 nodes.</span></span> <span data-ttu-id="4f52f-579">그렇지 않으면 10개 노드로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-579">Otherwise, it's set to 10 nodes.</span></span>

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a><span data-ttu-id="4f52f-580">예제2: 작업 기반 조정</span><span class="sxs-lookup"><span data-stu-id="4f52f-580">Example 2: Task-based adjustment</span></span>
<span data-ttu-id="4f52f-581">이 예에서는 풀 크기는 큐에 있는 작업의 수에 따라 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-581">In this example, the pool size is adjusted based on the number of tasks in the queue.</span></span> <span data-ttu-id="4f52f-582">주석과 줄 바꿈은 모두 수식 문자열에 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-582">Both comments and line breaks are acceptable in formula strings.</span></span>

```csharp
// Get pending tasks for the past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use the last sample point,
// otherwise we use the maximum of last sample point and the history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM to pending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// The pool size is capped at 20, if target VM value is more than that, set it
// to 20. This value should be adjusted according to your use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a><span data-ttu-id="4f52f-583">예제3: 병렬 작업에 대한 회계</span><span class="sxs-lookup"><span data-stu-id="4f52f-583">Example 3: Accounting for parallel tasks</span></span>
<span data-ttu-id="4f52f-584">이 예제에서는 작업의 수에 따라 풀 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-584">This example adjusts the pool size based on the number of tasks.</span></span> <span data-ttu-id="4f52f-585">이 수식은 또한 풀에 대해 설정된 [MaxTasksPerComputeNode][net_maxtasks] 값을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-585">This formula also takes into account the [MaxTasksPerComputeNode][net_maxtasks] value that has been set for the pool.</span></span> <span data-ttu-id="4f52f-586">이 방법은 [병렬 작업 실행](batch-parallel-node-tasks.md)이 풀에서 사용된 경우에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-586">This approach is useful in situations where [parallel task execution](batch-parallel-node-tasks.md) has been enabled on your pool.</span></span>

```csharp
// Determine whether 70 percent of the samples have been recorded in the past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set the number of nodes to add to one-fourth the number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set to 4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt to grow the number of compute nodes to match the number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep the nodes active until the tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a><span data-ttu-id="4f52f-587">예제4: 초기 풀 크기 설정</span><span class="sxs-lookup"><span data-stu-id="4f52f-587">Example 4: Setting an initial pool size</span></span>
<span data-ttu-id="4f52f-588">이 예제에서는 초기 기간 동안 풀 크기를 지정된 노드 수로 설정하는 자동 크기 조정 수식이 있는 C# 코드 조각을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-588">This example shows a C# code snippet with an autoscale formula that sets the pool size to a specified number of nodes for an initial time period.</span></span> <span data-ttu-id="4f52f-589">그런 다음 초기 기간이 경과한 후 실행 중이고 활성화된 작업 수를 기반으로 풀 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-589">Then it adjusts the pool size based on the number of running and active tasks after the initial time period has elapsed.</span></span>

<span data-ttu-id="4f52f-590">다음 코드 조각의 수식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-590">The formula in the following code snippet:</span></span>

* <span data-ttu-id="4f52f-591">초기 풀 크기를 4 노드로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-591">Sets the initial pool size to four nodes.</span></span>
* <span data-ttu-id="4f52f-592">풀의 수명 주기의 처음 10분 이내에는 풀 크기를 조정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-592">Does not adjust the pool size within the first 10 minutes of the pool's lifecycle.</span></span>
* <span data-ttu-id="4f52f-593">10분 후 지난 60분 이내에 실행 중이고 활성화된 작업 수의 최대값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-593">After 10 minutes, obtains the max value of the number of running and active tasks within the past 60 minutes.</span></span>
  * <span data-ttu-id="4f52f-594">두 값이 모두 0이면(마지막 60분 동안 실행 중이거나 활성화된 작업이 없었음을 나타냄) 풀 크기가 0입니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-594">If both values are 0 (indicating that no tasks were running or active in the last 60 minutes), the pool size is set to 0.</span></span>
  * <span data-ttu-id="4f52f-595">값 중 하나가 0보다 큰 경우 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-595">If either value is greater than zero, no change is made.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4f52f-596">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f52f-596">Next steps</span></span>
* <span data-ttu-id="4f52f-597">[동시 노드 작업으로 Azure 배치 계산 리소스 사용 극대화](batch-parallel-node-tasks.md) 는 풀의 계산 노드에서 여러 작업을 동시에 실행할 수 있는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-597">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) contains details about how you can execute multiple tasks simultaneously on the compute nodes in your pool.</span></span> <span data-ttu-id="4f52f-598">자동 크기 조정 외에도 이 기능은 일부 워크로드에 대한 작업 기간을 줄여서 비용을 절약하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-598">In addition to autoscaling, this feature may help to lower job duration for some workloads, saving you money.</span></span>
* <span data-ttu-id="4f52f-599">다른 효율성 부스터의 경우 배치 응용 프로그램이 배치 서비스를 최적화하여 쿼리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f52f-599">For another efficiency booster, ensure that your Batch application queries the Batch service in the most optimal way.</span></span> <span data-ttu-id="4f52f-600">잠재적으로 수천 개의 계산 노드 또는 작업의 상태를 쿼리할 때 네트워크를 교차하는 데이터의 양을 제한하는 방법을 알아보려면 [효율적인 Azure Batch 서비스 쿼리](batch-efficient-list-queries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f52f-600">See [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to learn how to limit the amount of data that crosses the wire when you query the status of potentially thousands of compute nodes or tasks.</span></span>

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
