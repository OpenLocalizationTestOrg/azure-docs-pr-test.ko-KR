---
title: "비용 효율적이며 우선 순위가 낮은 VM에서 Azure Batch 워크로드 실행(미리 보기) | Microsoft Docs"
description: "우선 순위가 낮은 VM을 프로비전하여 Azure Batch 워크로드의 비용을 줄이는 방법을 알아봅니다."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 9bf0ac322020d8a8453011c3207c1930175db6d3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="c8a96-103">Batch(미리 보기)에서 낮은 우선 순위 VM 사용</span><span class="sxs-lookup"><span data-stu-id="c8a96-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="c8a96-104">Azure 배치는 낮은 우선 순위 VM(가상 컴퓨터)을 사용하여 Batch 워크로드의 비용을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-104">Azure Batch offers low-priorty virtual machines (VMs) to reduce the cost of Batch workloads.</span></span> <span data-ttu-id="c8a96-105">우선 순위가 낮은 VM은 경제적 측면도 있는 대량의 Compute 성능을 제공하여 새로운 유형의 Batch 워크로드를 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="c8a96-106">우선 순위가 낮은 VM은 Azure에서 남는 용량을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="c8a96-107">풀에서 우선 순위가 낮은 VM을 지정하면 Azure Batch는 가능한 경우 이러한 남는 용량을 자동으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="c8a96-108">우선 순위가 낮은 VM을 사용할 경우 Azure에서 사용할 수 있는 추가 용량이 없을 때 해당 VM이 선점될 수 있다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-108">The tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="c8a96-109">이러한 이유로 우선 순위가 낮은 VM이 특정 유형의 워크로드에 가장 적절합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="c8a96-110">작업 완료 시간이 유연하고 작업이 여러 VM 간에 분산되는 Batch 및 비동기 처리 워크로드에 우선 순위가 낮은 BM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-110">Use low-priority VMs for batch and asynchronous processing workloads where the job completion time is flexible and the work is distributed across many VMs.</span></span>

<span data-ttu-id="c8a96-111">우선 순위가 낮은 VM은 전용 VM보다 훨씬 덜 비쌉니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="c8a96-112">가격 책정 세부 정보에 대해서는 [Batch 가격 책정](https://azure.microsoft.com/pricing/details/batch/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8a96-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="c8a96-113">우선 순위가 낮은 VM에 대한 추가 토론 내용을 보려면 [보다 저렴한 가격으로 일괄 컴퓨팅 수행](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8a96-113">For an additional discussion of low-priority VMs, see the blog post announcement: [Batch computing at a fraction of the price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8a96-114">우선 순위가 낮은 VM은 현재 미리 보기 상태이며 Batch에서 실행되는 워크로드에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="c8a96-115">우선 순위가 낮은 VM에 대한 사용 사례</span><span class="sxs-lookup"><span data-stu-id="c8a96-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="c8a96-116">우선 순위가 낮은 VM의 특성을 고려할 때 어떤 워크로드에 해당 VM을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="c8a96-116">Given the characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="c8a96-117">작업이 여러 병렬 태스크로 분할되거나, 많은 VM에서 확장 및 분산되는 많은 작업이 있으므로 일반적으로는 Batch 처리 워크로드가 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="c8a96-118">Azure에서 남는 용량을 최대한 활용하기 위해 적절한 작업을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-118">To maximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="c8a96-119">경우에 따라 VM을 사용할 수 없거나 선점되면 작업에 대한 용량이 줄어들어 태스크가 중단되고 다시 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead to task interruption and reruns.</span></span> <span data-ttu-id="c8a96-120">따라서 작업을 실행하는 데 걸리는 시간을 유연하게 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-120">Jobs must therefore be flexible in the time they can take to run.</span></span>

-   <span data-ttu-id="c8a96-121">좀 더 긴 태스크를 포함하는 작업은 중단될 경우 더 많은 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="c8a96-122">장기 실행 작업이 검사점 설정을 구현하여 실행될 때 진행 상황을 저장하는 경우 중단에 따른 영향이 훨씬 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-122">If long-running tasks implement checkpointing to save progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="c8a96-123">실행 시간이 더 짧은 태스크는 중단에 따른 영향이 훨씬 작아지므로 우선 순위가 낮은 VM에서 가장 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-123">Tasks with shorter execution times tend to work best with low-priority VMs as the impact of interruption is far less.</span></span>

-   <span data-ttu-id="c8a96-124">여러 VM을 활용하는 장기 실행 MPI 작업은 하나의 선점된 VM 때문에 전체 작업이 다시 실행되어야 하므로 우선 순위가 낮은 VM을 사용하는 것이 별로 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-124">Long-running MPI jobs that utilize multiple VMs are not well suited to use low-priority VMs as one preempted VM will likely lead to the whole job having to be run again.</span></span>

<span data-ttu-id="c8a96-125">Batch 처리 사용 사례의 일부 예제에는 우선 순위가 낮은 VM을 사용하는 것이 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-125">Some examples of batch processing use cases well suited to use low-priority VMs are:</span></span>

-   <span data-ttu-id="c8a96-126">**개발 및 테스트**: 특히 대규모 솔루션을 개발 중인 경우 상당한 비용 절감을 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="c8a96-127">모든 유형의 테스트가 혜택을 볼 수 있지만 대규모 부하 테스트 및 회귀 테스트에 사용하면 아주 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="c8a96-128">**요청 시 용량 보완**: 우선 순위가 낮은 VM은 일반적인 전용 VM을 보완하는 데 사용될 수 있습니다. 사용 가능한 경우 작업을 확장하여 더 낮은 비용으로 더 빠르게 완료할 수 있고, 사용 가능하지 않은 경우 전용 VM 수준만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, the baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="c8a96-129">**유연한 작업 실행 시간**: 작업이 완료되어야 하는 시간이 유연한 경우 잠재적인 용량 감소가 허용될 수 있지만 우선 순위가 낮은 VM을 추가하면 작업이 더 낮은 비용으로 더 빠르게 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-129">**Flexible job execution time**: If there is flexibility in the time jobs have to complete, then potential drops in capacity can be tolerated; however, with the addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="c8a96-130">Batch 풀은 작업 실행 시간의 유연성에 따라 몇 가지 방법으로 우선 순위가 낮은 VM을 사용하도록 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-130">Batch pools can be configured to use low-priority VMs in a few ways, depending on the flexibility in job execution time:</span></span>

-   <span data-ttu-id="c8a96-131">풀에서 우선 순위가 낮은 VM만 사용될 수 있고 Batch 기능은 사용 가능한 경우 선점된 용량을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="c8a96-132">이것이 우선 순위가 낮은 VM만 사용될 때 작업을 실행하는 가장 경제적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-132">This is the cheapest way to execute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="c8a96-133">우선 순위가 낮은 VM을 고정된 전용 VM과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="c8a96-134">고정된 전용 VM의 수가 있으면 항상 일정한 용량을 작업 처리에 사용할 수 있도록 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-134">The fixed number of dedicated VMs ensures there is always some capacity to keep a job progressing.</span></span>

-   <span data-ttu-id="c8a96-135">전용 VM과 우선 순위가 낮은 VM이 동적으로 혼합될 수 있으므로 사용 가능한 경우 좀 더 저렴한 우선 순위가 낮은 VM만 사용되고, 필요할 때는 높은 가격의 전용 VM을 확장하여 최소한의 용량으로 작업을 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but the full-priced dedicated VMs are scaled up when required, to keep a minimum amount of capacity available to keep the jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="c8a96-136">우선 순위가 낮은 VM에 대한 Batch 지원</span><span class="sxs-lookup"><span data-stu-id="c8a96-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="c8a96-137">Azure Batch는 우선 순위가 낮은 VM을 쉽게 활용하고 혜택을 얻을 수 있도록 하는 몇 가지 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-137">Azure Batch provides several capabilities that make it easy to consume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="c8a96-138">Batch 풀은 전용 VM 및 우선 순위가 낮은 VM을 모두 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="c8a96-139">각 유형의 VM 수는 풀이 만들어질 때 지정될 수 있으며, 기준 풀에 대해서는 명시적 크기 조정 작업이나 자동 크기 조정 기능을 사용해서 언제든지 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-139">The number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using the explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="c8a96-140">작업 및 태스크 전송은 변경되지 않은 상태로 유지되며 풀의 VM 유형과 관련된 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-140">Job and task submission can remain unchanged and do not need to be concerned with the VM types in the pool.</span></span> <span data-ttu-id="c8a96-141">작업을 가능한 한 경제적으로 실행할 수 있게 풀이 우선 순위가 낮은 VM을 완전히 사용하도록 할 수 있지만 용량이 최소 임계값 아래로 떨어질 경우 작업이 계속 실행되도록 하기 위해 전용 VM을 스핀업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-141">It is also possible to have a pool completely use low-priority VMs to run jobs as cheaply as possible, but spin up dedicated VMs if the capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="c8a96-142">Batch 풀은 목표 개수의 우선 순위가 낮은 VM을 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-142">Batch pools automatically seek to the target number of low-priority VMs.</span></span> <span data-ttu-id="c8a96-143">VM이 선점되면 Batch는 손실된 용량을 대체하고 목표 수준을 복구하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-143">If VMs are preempted, then Batch will attempt to replace the lost capacity and return to the target.</span></span>

-   <span data-ttu-id="c8a96-144">태스크가 중단된 경우 Batch는 태스크를 검색하고 다시 실행되도록 자동으로 다시 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-144">In the case of tasks being interrupted, Batch will detect and automatically requeue tasks to be run again.</span></span>

-   <span data-ttu-id="c8a96-145">우선 순위가 낮은 VM의 코어 할당량은 전용 VM과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="c8a96-146">우선 순위가 낮은 VM은 비용이 저렴하므로 할당량이 전용 VM보다 높습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-146">The quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="c8a96-147">자세한 내용은 [Batch 서비스 할당량 및 제한](batch-quota-limit.md#resource-quotas)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8a96-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="c8a96-148">우선 순위가 낮은 VM은 풀 할당 모드가 [사용자 구독](batch-account-create-portal.md#user-subscription-mode)으로 설정된 Batch 계정에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-148">Low-priority VMs are not currently supported for Batch accounts where the pool allocation mode is set to [User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="c8a96-149">풀 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="c8a96-149">Create and update pools</span></span>

<span data-ttu-id="c8a96-150">Batch 풀은 전용 VM 및 우선 순위가 낮은 VM(Compute 노드라고도 함)을 둘 다 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-150">A Batch pool can contain both dedicated and low-priority VMs (also referred to as compute nodes).</span></span> <span data-ttu-id="c8a96-151">전용 및 우선 순위가 낮은 VM 둘 다에 대해 Compute 노드의 목표 수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-151">You can set the target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="c8a96-152">목표 노드 수는 풀에 유지하려는 VM의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-152">The target number of nodes specifies the number of VMs you want to have in the pool.</span></span>

<span data-ttu-id="c8a96-153">예를 들어 전용 VM과 우선 순위가 낮은 VM의 목표 수가 각각 5개와 20개인 Azure Cloud Service VM을 사용하여 풀을 만들려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-153">For example, to create a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="c8a96-154">전용 VM과 우선 순위가 낮은 VM의 목표 수가 각각 5개와 20개인 Azure Virtual Machines(이 경우 Linux VM)을 사용하여 풀을 만들려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-154">To create a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="c8a96-155">전용 및 우선 순위가 낮은 VM 둘 다의 현재 노드 수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-155">You can get the current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="c8a96-156">풀 노드에는 해당 노드가 전용 VM인지 또는 우선 순위가 낮은 VM인지를 나타내는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-156">Pool nodes have a property to indicate if the node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="c8a96-157">풀의 하나 이상의 노드가 선점될 경우 풀에 대한 노드 나열 작업은 해당 노드를 계속 반환하고, 우선 순위가 낮은 노드의 현재 수는 변경되지 않지만 해당 노드는 **선점** 상태로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, the current number of low-priority nodes will remain unchanged, but those nodes will have their state set to the **Preempted** state.</span></span> <span data-ttu-id="c8a96-158">Batch는 대체 VM을 찾으려고 하고, 성공하면 노드는 새 노드처럼 **만드는 중**, **시작 중** 상태를 차례로 거쳐 태스크 실행에 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-158">Batch will attempt to find replacement VMs and, if successful, the nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="c8a96-159">우선 순위가 낮은 VM을 포함하는 풀 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c8a96-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="c8a96-160">전용 VM으로만 구성된 풀의 경우처럼, Resize 메서드를 호출하거나 자동 크기 조정을 사용하여 우선 순위가 낮은 VM을 포함하는 풀의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-160">As with pools solely consisting of dedicated VMs, it is possible to scale a pool containing low-priority VMs by calling the Resize method or by using auto-scale.</span></span>

<span data-ttu-id="c8a96-161">풀 크기 조정 작업은 **targetLowPriorityNodes** 값을 업데이트하는 두 번째 선택적 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-161">The pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="c8a96-162">풀 자동 크기 조정 수식은 우선 순위가 낮은 VM을 다음과 같이 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-162">The pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="c8a96-163">서비스 정의 변수 **$TargetLowPriorityNodes**의 값을 가져오거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-163">You can get or set the value of the service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="c8a96-164">서비스 정의 변수 **$CurrentLowPriorityNodes**의 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-164">You can get the value of the service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="c8a96-165">서비스 정의 변수 **$PreemptedNodeCount**의 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-165">You can get the value of the service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="c8a96-166">이 변수는 선점 상태의 노드 수를 반환하고 사용할 수 없는 선점된 노드 수에 따라 전용 노드의 수를 늘리거나 줄일 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-166">This variable returns the number of nodes in the preempted state and allows you to scale up or down the number of dedicated nodes, depending on the number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="c8a96-167">작업 및 태스크</span><span class="sxs-lookup"><span data-stu-id="c8a96-167">Jobs and tasks</span></span>

<span data-ttu-id="c8a96-168">작업 및 태스크는 우선 순위가 낮은 노드에 대한 지원을 거의 요구하지 않으며 다음만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-168">Jobs and tasks require very little support for low-priority nodes; the only support is as follows:</span></span>

-   <span data-ttu-id="c8a96-169">작업의 JobManagerTask 속성은 새 속성 **AllowLowPriorityNode**를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-169">The JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="c8a96-170">이 속성이 true이면 작업 관리자 태스크는 전용 또는 우선 순위가 낮은 노드에서 예약될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-170">When this property is true, the job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="c8a96-171">이 속성이 false이면 작업 관리자 태스크는 전용 노드에서만 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-171">If this property is false, the job manager task will be scheduled to a dedicated node only.</span></span>

-   <span data-ttu-id="c8a96-172">태스크 응용 프로그램에서는 [환경 변수](batch-compute-node-environment-variables.md)를 사용하여 해당 응용 프로그램이 우선 순위가 낮은 노드에서 실행되는지 또는 전용 노드에서 실행되는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-172">An [environment variable](batch-compute-node-environment-variables.md) is available to a task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="c8a96-173">환경 변수는 AZ_BATCH_NODE_IS_DEDICATED입니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-173">The environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="c8a96-174">선점 처리</span><span class="sxs-lookup"><span data-stu-id="c8a96-174">Handling preemption</span></span>

<span data-ttu-id="c8a96-175">VM은 경우에 따라 선점될 수 있습니다. 이 경우 Batch는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-175">VMs may occasionally be preempted; when this happens, Batch does the following:</span></span>

-   <span data-ttu-id="c8a96-176">선점된 VM의 상태는 **선점됨**으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-176">The preempted VMs have their state updated to **Preempted**.</span></span>
-   <span data-ttu-id="c8a96-177">작업이 선점된 노드 VM에서 실행되면 해당 작업이 요청되고 다시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-177">If tasks were running on the preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="c8a96-178">VM은 효과적으로 삭제되므로 VM에 로컬로 저장된 모든 데이터는 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-178">The VM is effectively deleted, leading to any data stored locally on the VM being lost.</span></span>
-   <span data-ttu-id="c8a96-179">풀은 계속해서 우선 순위가 낮은 노드의 목표 개수가 사용 가능해지도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-179">The pool continually attempts to reach the target number of low-priority nodes available.</span></span> <span data-ttu-id="c8a96-180">대체 용량이 발견되면 노드는 해당 ID를 유지하지만 다시 초기화되며, 작업 예약에 사용되기 전에 먼저 **만드는 중** 및 **시작 중** 상태를 거치게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="c8a96-181">선점 수는 Azure Portal에서 메트릭으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-181">Preemption counts are available as a metric in the Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="c8a96-182">메트릭</span><span class="sxs-lookup"><span data-stu-id="c8a96-182">Metrics</span></span>

<span data-ttu-id="c8a96-183">우선 순위가 낮은 노드의 경우 [Azure Portal](https://portal.azure.com)에서 새 메트릭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-183">New metrics are available in the [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="c8a96-184">이러한 메트릭은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-184">These metrics are:</span></span>

- <span data-ttu-id="c8a96-185">우선 순위가 낮은 노드 수</span><span class="sxs-lookup"><span data-stu-id="c8a96-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="c8a96-186">우선 순위가 낮은 코어 수</span><span class="sxs-lookup"><span data-stu-id="c8a96-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="c8a96-187">선점된 노드 수</span><span class="sxs-lookup"><span data-stu-id="c8a96-187">Preempted Node Count</span></span>

<span data-ttu-id="c8a96-188">Azure Portal에서 메트릭을 확인하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-188">To view metrics in the Azure portal:</span></span>

1. <span data-ttu-id="c8a96-189">Portal에서 배치 계정으로 이동하여 배치 계정의 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-189">Navigate to your Batch account in the portal, and view the settings for your Batch account.</span></span>
2. <span data-ttu-id="c8a96-190">**모니터링** 섹션에서 **메트릭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-190">Select **Metrics** from the **Monitoring** section.</span></span>
3. <span data-ttu-id="c8a96-191">**사용 가능한 메트릭** 목록에서 원하는 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-191">Select the metrics you desire from the **Available Metrics** list.</span></span>

![우선 순위가 낮은 노드의 메트릭](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="c8a96-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c8a96-193">Next steps</span></span>

* <span data-ttu-id="c8a96-194">배치를 사용하려는 사용자를 위한 중요한 정보는 [개발자를 위한 배치 기능 개요](batch-api-basics.md)를 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-194">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="c8a96-195">문서에는 배치 응용 프로그램을 빌드하는 동안 사용할 수 있는 풀, 노드, 작업 및 태스크와 같은 배치 서비스 리소스 및 여러 API 기능에 대한 자세한 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-195">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="c8a96-196">Batch 솔루션을 빌드하는 데 사용할 수 있는 [Batch API 및 도구](batch-apis-tools.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c8a96-196">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
