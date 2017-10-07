---
title: "aaaRun Azure 일괄 처리 작업에 비용 효율적인 우선 순위가 낮은 Vm (미리 보기) | Microsoft Docs"
description: "Azure 일괄 처리 작업의 tooprovision 우선 순위가 낮은 Vm tooreduce hello 비용 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="a8468-103">Batch(미리 보기)에서 낮은 우선 순위 VM 사용</span><span class="sxs-lookup"><span data-stu-id="a8468-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="a8468-104">Azure 일괄 처리는 일괄 처리 작업의 낮은 우선 순위 가상 컴퓨터 (Vm) tooreduce hello 비용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-104">Azure Batch offers low-priorty virtual machines (VMs) tooreduce hello cost of Batch workloads.</span></span> <span data-ttu-id="a8468-105">우선 순위가 낮은 VM은 경제적 측면도 있는 대량의 Compute 성능을 제공하여 새로운 유형의 Batch 워크로드를 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="a8468-106">우선 순위가 낮은 VM은 Azure에서 남는 용량을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="a8468-107">풀에서 우선 순위가 낮은 VM을 지정하면 Azure Batch는 가능한 경우 이러한 남는 용량을 자동으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="a8468-108">이 경우 Vm 낮은 우선 순위를 사용 하기 위한 hello 단점이 과도 한 용량은 Azure에서 제공 하는 경우에 해당 Vm을 선점 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-108">hello tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="a8468-109">이러한 이유로 우선 순위가 낮은 VM이 특정 유형의 워크로드에 가장 적절합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="a8468-110">Vm 낮은 우선 순위를 사용 하 여 일괄 처리 및 비동기 처리 작업은 유연 hello 작업 완료 시간 및 hello 작업 많은 Vm을 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-110">Use low-priority VMs for batch and asynchronous processing workloads where hello job completion time is flexible and hello work is distributed across many VMs.</span></span>

<span data-ttu-id="a8468-111">우선 순위가 낮은 VM은 전용 VM보다 훨씬 덜 비쌉니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="a8468-112">가격 책정 세부 정보에 대해서는 [Batch 가격 책정](https://azure.microsoft.com/pricing/details/batch/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8468-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="a8468-113">Vm 낮은 우선 순위는 추가 논의 알려면 hello 블로그 게시물 공지: [hello 가격의 일부분에 컴퓨팅 일괄 처리](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-113">For an additional discussion of low-priority VMs, see hello blog post announcement: [Batch computing at a fraction of hello price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8468-114">우선 순위가 낮은 VM은 현재 미리 보기 상태이며 Batch에서 실행되는 워크로드에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="a8468-115">우선 순위가 낮은 VM에 대한 사용 사례</span><span class="sxs-lookup"><span data-stu-id="a8468-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="a8468-116">우선 순위가 낮은 Vm의 hello 특성, 어떤 작업 수와으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-116">Given hello characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="a8468-117">작업이 여러 병렬 태스크로 분할되거나, 많은 VM에서 확장 및 분산되는 많은 작업이 있으므로 일반적으로는 Batch 처리 워크로드가 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="a8468-118">Azure, 적합 한 작업에 과도 한 용량 toomaximize 사용 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-118">toomaximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="a8468-119">경우에 따라 Vm 사용 하지 못할 또는 있는 작업에 대 한 용량을 감소 되 고 tootask 중단 및 트리거하는지 않을 선점 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead tootask interruption and reruns.</span></span> <span data-ttu-id="a8468-120">따라서 작업 유연한 toorun 많이 hello 시간 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-120">Jobs must therefore be flexible in hello time they can take toorun.</span></span>

-   <span data-ttu-id="a8468-121">좀 더 긴 태스크를 포함하는 작업은 중단될 경우 더 많은 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="a8468-122">장기 실행 작업 실행 검사점 toosave 진행 상황을 구현 하는 경우 다음 중단의 영향 것 훨씬 적습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-122">If long-running tasks implement checkpointing toosave progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="a8468-123">실행 시간이 짧은 작업 간격과 toowork 가장 우선 순위가 낮은 Vm과 중단의 hello 영향은 훨씬 적습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-123">Tasks with shorter execution times tend toowork best with low-priority VMs as hello impact of interruption is far less.</span></span>

-   <span data-ttu-id="a8468-124">여러 Vm을 활용 하는 MPI 작업에 가장 적합된 toouse 없는 장기 실행 선점된 하나의 VM으로 우선 순위가 낮은 Vm 가능성이 높은 잠재 고객 toohello 전체 작업을 다시 실행 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-124">Long-running MPI jobs that utilize multiple VMs are not well suited toouse low-priority VMs as one preempted VM will likely lead toohello whole job having toobe run again.</span></span>

<span data-ttu-id="a8468-125">일괄 처리의 몇 가지 예의 경우에 가장 적합된 toouse vm 낮은 우선 순위를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-125">Some examples of batch processing use cases well suited toouse low-priority VMs are:</span></span>

-   <span data-ttu-id="a8468-126">**개발 및 테스트**: 특히 대규모 솔루션을 개발 중인 경우 상당한 비용 절감을 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="a8468-127">모든 유형의 테스트가 혜택을 볼 수 있지만 대규모 부하 테스트 및 회귀 테스트에 사용하면 아주 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="a8468-128">**요청 시 용량 보완**: regular 전용된 Vm-보완 하기 위해 Vm 낮은 우선 순위를 사용할 수 작업의 크기를 조정 하 고 따라서 저렴 한 비용에 대 한 훨씬 더 빠르게 완료 수, 사용 가능한 경우; 때의 전용을 사용할 수 없는 hello 초기 Vm을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, hello baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="a8468-129">**유연한 작업 실행 시간**: hello 타이머 작업이 더 유연성을 제공 하는 경우 toocomplete, 한 다음 잠재적인 용량 감소 허용 될 수 있으며 단, hello로 우선 순위가 낮은 Vm 작업의 추가 자주 실행 빠르고 저렴 한 비용에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-129">**Flexible job execution time**: If there is flexibility in hello time jobs have toocomplete, then potential drops in capacity can be tolerated; however, with hello addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="a8468-130">일괄 처리 풀의 hello 유연성에 따라 몇 가지 방법으로 우선 순위가 낮은 Vm 작업 실행 시간이 구성 된 toouse 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-130">Batch pools can be configured toouse low-priority VMs in a few ways, depending on hello flexibility in job execution time:</span></span>

-   <span data-ttu-id="a8468-131">풀에서 우선 순위가 낮은 VM만 사용될 수 있고 Batch 기능은 사용 가능한 경우 선점된 용량을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="a8468-132">이 hello 가장 저렴 한 방식으로 tooexecute 작업만 우선 순위가 낮은 Vm에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-132">This is hello cheapest way tooexecute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="a8468-133">우선 순위가 낮은 VM을 고정된 전용 VM과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="a8468-134">hello 전용된 Vm의 고정 된 수 있는지 확인할 일부 용량 tookeep 항상 작업 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-134">hello fixed number of dedicated VMs ensures there is always some capacity tookeep a job progressing.</span></span>

-   <span data-ttu-id="a8468-135">사용 가능한 경우 더 저렴 우선 순위가 낮은 Vm 전적으로 사용 되지만 필요한 경우 tookeep 용량 사용 가능한 tookeep hello 작업의 최소 크기를 확장 하는 전용 전체 가격이 책정 hello Vm 수 있도록 동적 조합의 전용 및 우선 순위가 낮은 Vm 수 있습니다. 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but hello full-priced dedicated VMs are scaled up when required, tookeep a minimum amount of capacity available tookeep hello jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="a8468-136">우선 순위가 낮은 VM에 대한 Batch 지원</span><span class="sxs-lookup"><span data-stu-id="a8468-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="a8468-137">Azure 배치 쉽게 tooconsume 확인 하 고 우선 순위가 낮은 Vm에서 활용 하는 몇 가지 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-137">Azure Batch provides several capabilities that make it easy tooconsume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="a8468-138">Batch 풀은 전용 VM 및 우선 순위가 낮은 VM을 모두 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="a8468-139">풀을 생성 하거나 언제 든 지 자동 크기 조정 또는 안녕하세요 명시적 크기 조정 작업을 사용 하 여 기존 풀에 대 한 변경할 hello 각 유형의 VM 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-139">hello number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using hello explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="a8468-140">작업 및 태스크 전송 변경 되지 않고 남아 있을 수 및 hello 풀의 hello VM 유형에 신경 쓸 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-140">Job and task submission can remain unchanged and do not need to be concerned with hello VM types in hello pool.</span></span> <span data-ttu-id="a8468-141">풀을 완전히 우선 순위가 낮은 Vm toorun 작업 사용 가능 하지만 Vm 전용된 회전 저렴 hello 용량 실행 중인 작업을 유지 하는 최소 임계값 아래로 떨어지는 경우 가능한 toohave 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-141">It is also possible toohave a pool completely use low-priority VMs toorun jobs as cheaply as possible, but spin up dedicated VMs if hello capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="a8468-142">일괄 처리 풀 Vm 낮은 우선 순위 toohello 대상 수를 자동으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-142">Batch pools automatically seek toohello target number of low-priority VMs.</span></span> <span data-ttu-id="a8468-143">Vm 선점 된 경우 일괄 처리 용량 및 반환 toohello 대상 손실 tooreplace hello를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-143">If VMs are preempted, then Batch will attempt tooreplace hello lost capacity and return toohello target.</span></span>

-   <span data-ttu-id="a8468-144">Hello 중단 되 고 작업의 경우에서 일괄 처리에서는 검색 하 고 자동으로 다시 실행 작업 toobe 내용을 알리게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-144">In hello case of tasks being interrupted, Batch will detect and automatically requeue tasks toobe run again.</span></span>

-   <span data-ttu-id="a8468-145">우선 순위가 낮은 VM의 코어 할당량은 전용 VM과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="a8468-146">우선 순위가 낮은 Vm에 대 한 인용 hello 우선 순위가 낮은 Vm 비용을 줄일 때문에 전용된 Vm의 보다 최신입니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-146">hello quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="a8468-147">자세한 내용은 [Batch 서비스 할당량 및 제한](batch-quota-limit.md#resource-quotas)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8468-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="a8468-148">우선 순위가 낮은 Vm 너무 hello 풀 할당 모드가 설정 되어 있는 일괄 처리 계정에 대 한 현재 지원 되지 않는[사용자 구독](batch-account-create-portal.md#user-subscription-mode)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-148">Low-priority VMs are not currently supported for Batch accounts where hello pool allocation mode is set too[User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="a8468-149">풀 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="a8468-149">Create and update pools</span></span>

<span data-ttu-id="a8468-150">일괄 처리 풀 전용 및 우선 순위가 낮은 Vm (또한 참조 tooas 계산 노드)를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-150">A Batch pool can contain both dedicated and low-priority VMs (also referred tooas compute nodes).</span></span> <span data-ttu-id="a8468-151">전용 및 우선 순위가 낮은 Vm에 대 한 계산 노드의 hello 대상 수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-151">You can set hello target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="a8468-152">hello 노드 수가 대상 수를 지정 hello toohave hello 풀에서 원하는 Vm의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-152">hello target number of nodes specifies hello number of VMs you want toohave in hello pool.</span></span>

<span data-ttu-id="a8468-153">예를 들어 5의 대상을 사용 하 여 Azure 클라우드 서비스 Vm을 사용 하 여 풀 a toocreate Vm과 20 대의 우선 순위가 낮은 Vm 전용:</span><span class="sxs-lookup"><span data-stu-id="a8468-153">For example, toocreate a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="a8468-154">5의 대상을 사용 하 여 (이 경우 Linux Vm)에서 Azure 가상 컴퓨터를 사용 하 여 풀 a toocreate Vm과 20 대의 우선 순위가 낮은 Vm 전용:</span><span class="sxs-lookup"><span data-stu-id="a8468-154">toocreate a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="a8468-155">전용 및 우선 순위가 낮은 Vm에 대 한 hello 현재 노드 수를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-155">You can get hello current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="a8468-156">풀 노드 속성 tooindicate 있으면 hello 노드는 전용 또는 우선 순위가 낮은 VM:</span><span class="sxs-lookup"><span data-stu-id="a8468-156">Pool nodes have a property tooindicate if hello node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="a8468-157">선점 된 풀에서 하나 이상의 노드, 풀에는 목록 노드 작업은 해당 노드의 반환 여전히, hello 현재 우선 순위가 낮은 노드 수가 동일할 것 있지만 이러한 노드는 상태로 설정 toothe **프로그램 바뀜**상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, hello current number of low-priority nodes will remain unchanged, but those nodes will have their state set toothe **Preempted** state.</span></span> <span data-ttu-id="a8468-158">일괄 처리는 Vm toofind 대체를 시도 하 고 hello 노드를 통과 성공 하면 **만들기** 차례로 **시작** 상태 작업 실행을 위해 사용할 수 있게 되기 전에 새 노드에서 동일 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-158">Batch will attempt toofind replacement VMs and, if successful, hello nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="a8468-159">우선 순위가 낮은 VM을 포함하는 풀 크기 조정</span><span class="sxs-lookup"><span data-stu-id="a8468-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="a8468-160">전적으로 전용된 Vm으로 구성 된 풀에서와 마찬가지로 hello 크기 조정 메서드를 호출 하 여 또는 자동 크기 조정에 사용 하 여 가능한 tooscale는 풀 포함 우선 순위가 낮은 Vm 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-160">As with pools solely consisting of dedicated VMs, it is possible tooscale a pool containing low-priority VMs by calling hello Resize method or by using auto-scale.</span></span>

<span data-ttu-id="a8468-161">hello 풀 크기 조정 작업 두 번째 선택적 매개 변수 값을 업데이트 하는 **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="a8468-161">hello pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="a8468-162">hello 풀 자동 크기 조정 수식을 다음과 같이 Vm 낮은 우선 순위를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-162">hello pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="a8468-163">가져오거나 hello hello 서비스 정의 된 변수 값을 설정할 수 **$TargetLowPriorityNodes**합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-163">You can get or set hello value of hello service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="a8468-164">Hello 서비스 정의 변수의 hello 값을 얻을 수 **$CurrentLowPriorityNodes**합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-164">You can get hello value of hello service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="a8468-165">Hello 서비스 정의 변수의 hello 값을 얻을 수 **$PreemptedNodeCount**합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-165">You can get hello value of hello service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="a8468-166">이 변수는 hello hello의 노드 수가 선점 상태 및 사용할 수 없는 선점된 노드 hello 수에 따라 전용 노드의 hello 수의 위아래로 조정할 수 있습니다를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-166">This variable returns hello number of nodes in hello preempted state and allows you to scale up or down hello number of dedicated nodes, depending on hello number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="a8468-167">작업 및 태스크</span><span class="sxs-lookup"><span data-stu-id="a8468-167">Jobs and tasks</span></span>

<span data-ttu-id="a8468-168">작업 및 작업에 대 한 우선 순위가 낮은 노드; 거의 지원이 필요 hello 지원만는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-168">Jobs and tasks require very little support for low-priority nodes; hello only support is as follows:</span></span>

-   <span data-ttu-id="a8468-169">hello JobManagerTask 속성 작업의 새 속성이 **AllowLowPriorityNode**합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-169">hello JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="a8468-170">이 속성이 true 이면 전용 또는 우선 순위가 낮은 노드에 hello 작업 관리자 태스크를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-170">When this property is true, hello job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="a8468-171">이 속성이 false 이면 hello 작업 관리자 태스크 예약된 tooa 전용된 노드에서만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-171">If this property is false, hello job manager task will be scheduled tooa dedicated node only.</span></span>

-   <span data-ttu-id="a8468-172">[환경 변수](batch-compute-node-environment-variables.md) 는 사용할 수 있는 tooa 작업 응용 프로그램 우선 순위가 낮은 또는 전용 노드에서 실행 되 고 있는지 여부를 결정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-172">An [environment variable](batch-compute-node-environment-variables.md) is available tooa task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="a8468-173">hello 환경 변수가 AZ_BATCH_NODE_IS_DEDICATED 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-173">hello environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="a8468-174">선점 처리</span><span class="sxs-lookup"><span data-stu-id="a8468-174">Handling preemption</span></span>

<span data-ttu-id="a8468-175">Vm 수 선점 될 경우에 따라; 이 경우 일괄 처리는 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="a8468-175">VMs may occasionally be preempted; when this happens, Batch does hello following:</span></span>

-   <span data-ttu-id="a8468-176">hello 선점된 Vm 상태에 있는 해당 업데이트**프로그램 바뀜**합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-176">hello preempted VMs have their state updated too**Preempted**.</span></span>
-   <span data-ttu-id="a8468-177">작업에서 실행 되 던 작업은 다시 대기 하 고 다시 실행 hello 노드 Vm을 선점.</span><span class="sxs-lookup"><span data-stu-id="a8468-177">If tasks were running on hello preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="a8468-178">hello VM 효과적으로 삭제 됩니다 업계 최고의 tooany 데이터 hello 손실 되는 VM에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-178">hello VM is effectively deleted, leading tooany data stored locally on hello VM being lost.</span></span>
-   <span data-ttu-id="a8468-179">hello 풀 지속적으로 사용할 수 있는 우선 순위가 낮은 노드 tooreach hello 대상 수를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-179">hello pool continually attempts tooreach hello target number of low-priority nodes available.</span></span> <span data-ttu-id="a8468-180">대체 용량이 발견되면 노드는 해당 ID를 유지하지만 다시 초기화되며, 작업 예약에 사용되기 전에 먼저 **만드는 중** 및 **시작 중** 상태를 거치게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="a8468-181">선점 수는 hello Azure 포털에서에서를 기준으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-181">Preemption counts are available as a metric in hello Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="a8468-182">메트릭</span><span class="sxs-lookup"><span data-stu-id="a8468-182">Metrics</span></span>

<span data-ttu-id="a8468-183">Hello에 사용할 수 있는 새 메트릭이 [Azure 포털](https://portal.azure.com) 우선 순위가 낮은 노드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-183">New metrics are available in hello [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="a8468-184">이러한 메트릭은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-184">These metrics are:</span></span>

- <span data-ttu-id="a8468-185">우선 순위가 낮은 노드 수</span><span class="sxs-lookup"><span data-stu-id="a8468-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="a8468-186">우선 순위가 낮은 코어 수</span><span class="sxs-lookup"><span data-stu-id="a8468-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="a8468-187">선점된 노드 수</span><span class="sxs-lookup"><span data-stu-id="a8468-187">Preempted Node Count</span></span>

<span data-ttu-id="a8468-188">hello Azure 포털에서에서 tooview 메트릭:</span><span class="sxs-lookup"><span data-stu-id="a8468-188">tooview metrics in hello Azure portal:</span></span>

1. <span data-ttu-id="a8468-189">Hello 포털에서 일괄 처리 계정 tooyour를 탐색 하 고 일괄 처리 계정에 대 한 hello 설정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-189">Navigate tooyour Batch account in hello portal, and view hello settings for your Batch account.</span></span>
2. <span data-ttu-id="a8468-190">선택 **메트릭** hello에서 **모니터링** 섹션.</span><span class="sxs-lookup"><span data-stu-id="a8468-190">Select **Metrics** from hello **Monitoring** section.</span></span>
3. <span data-ttu-id="a8468-191">Hello에서 원하는 hello 메트릭을 선택 **사용 가능한 메트릭** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-191">Select hello metrics you desire from hello **Available Metrics** list.</span></span>

![우선 순위가 낮은 노드의 메트릭](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="a8468-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8468-193">Next steps</span></span>

* <span data-ttu-id="a8468-194">읽기 hello [개발자를 위한 일괄 처리 기능 개요](batch-api-basics.md), toouse 일괄 처리를 준비 하 고 모든 사용자에 대 한 필수 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-194">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="a8468-195">hello 문서 풀, 노드, 작업 및 작업, 및 hello와 같은 일괄 처리 서비스 리소스에 대 한 자세한 내용은 일괄 처리 응용 프로그램을 작성 하는 동안 사용할 수 있는 많은 API 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-195">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="a8468-196">Hello에 대 한 자세한 내용은 [일괄 처리 Api와 도구](batch-apis-tools.md) 일괄 처리 솔루션을 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8468-196">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
