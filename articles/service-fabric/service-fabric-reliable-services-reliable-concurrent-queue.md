---
title: "Azure Service Fabric의 ReliableConcurrentQueue"
description: "ReliableConcurrentQueue는 병렬 큐에 추가하고 큐에서 제거할 수 있는 처리량이 높은 큐입니다."
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 122cb48149477f295a65b8ee623c647b6db10a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-reliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="865f5-103">Azure Service Fabric의 ReliableConcurrentQueue 소개</span><span class="sxs-lookup"><span data-stu-id="865f5-103">Introduction to ReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="865f5-104">신뢰할 수 있는 동시 큐는 비동기, 트랜잭션 및 복제된 큐로서 큐에 넣기 및 큐에서 제거 작업에 대한 높은 동시성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="865f5-105">[신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx)에서 제공한 엄격한 FIFO 순서를 완화하여 처리량이 높고 대기 시간이 짧게 설계되었으며 대신 최상의 순서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-105">It is designed to deliver high throughput and low latency by relaxing the strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="865f5-106">API</span><span class="sxs-lookup"><span data-stu-id="865f5-106">APIs</span></span>

|<span data-ttu-id="865f5-107">동시 큐</span><span class="sxs-lookup"><span data-stu-id="865f5-107">Concurrent Queue</span></span>                |<span data-ttu-id="865f5-108">신뢰할 수 있는 동시 큐</span><span class="sxs-lookup"><span data-stu-id="865f5-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="865f5-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="865f5-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="865f5-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="865f5-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="865f5-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="865f5-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="865f5-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="865f5-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="865f5-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="865f5-113">int Count()</span></span>                    | <span data-ttu-id="865f5-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="865f5-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="865f5-115">[신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx)와 비교</span><span class="sxs-lookup"><span data-stu-id="865f5-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="865f5-116">신뢰할 수 있는 동시 큐는 [신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx)에 대한 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-116">Reliable Concurrent Queue is offered as an alternative to [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="865f5-117">FIFO 보장은 동시성을 상쇄해야 하기 때문에 엄격한 FIFO 순서가 필요하지 않은 경우에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="865f5-118">[신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx)는 잠금을 사용하여 큐에 넣을 수 있는 최대 트랜잭션 및 한 번에 큐에서 제거하도록 허용되는 최대 트랜잭션 순으로 FIFO 순서를 강제합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks to enforce FIFO ordering, with at most one transaction allowed to enqueue and at most one transaction allowed to dequeue at a time.</span></span> <span data-ttu-id="865f5-119">비교에서 신뢰할 수 있는 동시 큐는 정렬 제약 조건을 완화하고 어떤 수의 동시 트랜잭션이 해당 큐에 넣기 및 큐에서 제거 작업을 인터리브하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-119">In comparison, Reliable Concurrent Queue relaxes the ordering constraint and allows any number concurrent transactions to interleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="865f5-120">가장 효율적인 순서를 제공하지만 신뢰할 수 있는 동시 큐에 있는 두 값의 상대적 순서를 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-120">Best-effort ordering is provided, however the relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="865f5-121">여러 동시 트랜잭션이 큐에 넣기 및/또는 큐에서 제거를 수행할 때 신뢰할 수 있는 동시 큐는 [신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx)보다 처리량이 높고 대기 시간이 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="865f5-122">ReliableConcurrentQueue의 샘플 사용 사례는 [메시지 큐](https://en.wikipedia.org/wiki/Message_queue) 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-122">A sample use case for the ReliableConcurrentQueue is the [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="865f5-123">이 시나리오에서 한 명 이상의 메시지 생산자는 항목을 만들고 큐에 추가하며 한 명 이상의 메시지 소비자는 큐에서 메시지를 끌어오고 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-123">In this scenario, one or more message producers create and add items to the queue, and one or more message consumers pull messages from the queue and process them.</span></span> <span data-ttu-id="865f5-124">여러 생산자 및 소비자는 큐를 처리하기 위해 동시 트랜잭션을 사용하여 독립적으로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-124">Multiple producers and consumers can work independently, using concurrent transactions in order to process the queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="865f5-125">사용 지침</span><span class="sxs-lookup"><span data-stu-id="865f5-125">Usage Guidelines</span></span>
* <span data-ttu-id="865f5-126">큐에 있는 항목의 보존 기간이 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-126">The queue expects that the items in the queue have a low retention period.</span></span> <span data-ttu-id="865f5-127">즉, 항목은 오랜 시간 동안 큐에 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-127">That is, the items would not stay in the queue for a long time.</span></span>
* <span data-ttu-id="865f5-128">큐는 엄격한 FIFO 순서를 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-128">The queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="865f5-129">큐는 고유한 쓰기를 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-129">The queue does not read its own writes.</span></span> <span data-ttu-id="865f5-130">항목이 트랜잭션 내에서 큐에 삽입된 경우 동일한 트랜잭션 내에서 큐에서 제거하는 사용자에게 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-130">If an item is enqueued within a transaction, it will not be visible to a dequeuer within the same transaction.</span></span>
* <span data-ttu-id="865f5-131">큐에서 제거는 서로 분리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="865f5-132">항목 *A*가 트랜잭션 *txnA*라는 큐에서 제거된 경우 *txnA*가 커밋되지 않더라도 항목 *A*는 동시 트랜잭션 *txnB*에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible to a concurrent transaction *txnB*.</span></span>  <span data-ttu-id="865f5-133">*txnA*가 중단되면 *txnB*에서 즉시 *A*를 볼 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-133">If *txnA* aborts, *A* will become visible to *txnB* immediately.</span></span>
* <span data-ttu-id="865f5-134">*TryPeekAsync* 동작은 *TryDequeueAsync*를 사용한 다음 트랜잭션을 중단하여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="865f5-135">이러한 예는 프로그래밍 패턴 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-135">An example of this can be found in the Programming Patterns section.</span></span>
* <span data-ttu-id="865f5-136">개수는 비트랜잭션입니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-136">Count is non-transactional.</span></span> <span data-ttu-id="865f5-137">큐에서 요소의 수를 추측하는 데 사용할 수 있지만 특정 시점을 나타내며 의존할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-137">It can be used to get an idea of the number of elements in the queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="865f5-138">큐에서 제거된 항목에서 비용이 많이 드는 처리는 시스템의 성능에 영향을 줄 수 있는 장기 실행 트랜잭션을 방지하기 위해 트랜잭션이 활성화된 동안 수행하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-138">Expensive processing on the dequeued items should not be performed while the transaction is active, to avoid long-running transactions which may have a performance impact on the system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="865f5-139">코드 조각</span><span class="sxs-lookup"><span data-stu-id="865f5-139">Code Snippets</span></span>
<span data-ttu-id="865f5-140">몇 가지 코드 조각 및 예상된 출력에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="865f5-141">이 섹션에서 예외 처리는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="865f5-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="865f5-142">EnqueueAsync</span></span>
<span data-ttu-id="865f5-143">다음은 예상된 출력 뒤에 EnqueueAsync를 사용하기 위한 몇 가지 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="865f5-144">*사례 1: 단일 큐에 넣기 작업*</span><span class="sxs-lookup"><span data-stu-id="865f5-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="865f5-145">작업이 성공적으로 완료되고 큐를 수정하는 동시 트랜잭션이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-145">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="865f5-146">사용자는 다음 순서 중 하나로 항목을 포함하는 큐를 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-146">The user can expect the queue to contain the items in any of the following orders:</span></span>

> <span data-ttu-id="865f5-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="865f5-147">10, 20</span></span>

> <span data-ttu-id="865f5-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="865f5-148">20, 10</span></span>


- <span data-ttu-id="865f5-149">*사례 2: 병렬 큐에 넣기 작업*</span><span class="sxs-lookup"><span data-stu-id="865f5-149">*Case 2: Parallel Enqueue Task*</span></span>

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="865f5-150">작업이 성공적으로 완료되고, 작업이 병렬로 실행되고, 큐를 수정하는 다른 동시 트랜잭션이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-150">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="865f5-151">큐에 있는 항목의 순서를 방해할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-151">No inference can be made about the order of items in the queue.</span></span> <span data-ttu-id="865f5-152">이 코드 조각에 대 한 항목은 4에 나타날 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="865f5-152">For this code snippet, the items may appear in any of the 4!</span></span> <span data-ttu-id="865f5-153">가능한 순서로 정렬 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-153">possible orderings.</span></span>  <span data-ttu-id="865f5-154">큐는 원래 (큐에 넣은) 순서로 항목을 유지하려고 하지만 오류 또는 동시 작업으로 인해 순서를 변경해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-154">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="865f5-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="865f5-155">DequeueAsync</span></span>
<span data-ttu-id="865f5-156">다음은 예상된 출력 뒤에 TryDequeueAsync를 사용하기 위한 몇 가지 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-156">Here are a few code snippets for using TryDequeueAsync followed by the expected outputs.</span></span> <span data-ttu-id="865f5-157">큐가 이미 큐의 다음 항목으로 채워졌다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-157">Assume that the queue is already populated with the following items in the queue:</span></span>
> <span data-ttu-id="865f5-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="865f5-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="865f5-159">*사례 1: 단일 큐에서 제거 작업*</span><span class="sxs-lookup"><span data-stu-id="865f5-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="865f5-160">작업이 성공적으로 완료되고 큐를 수정하는 동시 트랜잭션이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-160">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="865f5-161">큐에 있는 항목의 순서를 방해할 수 없으므로 3개의 모든 항목은 순서에 관계없이 제거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-161">Since no inference can be made about the order of the items in the queue, any three of the items may be dequeued, in any order.</span></span> <span data-ttu-id="865f5-162">큐는 원래 (큐에 넣은) 순서로 항목을 유지하려고 하지만 오류 또는 동시 작업으로 인해 순서를 변경해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-162">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>  

- <span data-ttu-id="865f5-163">*사례 2: 병렬 큐에서 제거 작업*</span><span class="sxs-lookup"><span data-stu-id="865f5-163">*Case 2: Parallel Dequeue Task*</span></span>

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

<span data-ttu-id="865f5-164">작업이 성공적으로 완료되고, 작업이 병렬로 실행되고, 큐를 수정하는 다른 동시 트랜잭션이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-164">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="865f5-165">큐에 있는 항목의 순서를 방해할 수 없으므로 *dequeue1* 및 *dequeue2* 목록은 순서에 관계없이 각각 두 개의 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-165">Since no inference can be made about the order of the items in the queue, the lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="865f5-166">동일한 항목은 두 목록에 모두 표시되지 *않습니다*.</span><span class="sxs-lookup"><span data-stu-id="865f5-166">The same item will *not* appear in both lists.</span></span> <span data-ttu-id="865f5-167">따라서 dequeue1에 *10*, *30*이 있으면 dequeue2에는 *20*, *40*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="865f5-168">*사례 3: 트랜잭션이 중단된 큐에서 제거 순서*</span><span class="sxs-lookup"><span data-stu-id="865f5-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="865f5-169">진행 중인 큐에서 제거를 포함한 트랜잭션을 중단하면 항목을 큐의 시작 부분에 다시 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-169">Aborting a transaction with in-flight dequeues puts the items back on the head of the queue.</span></span> <span data-ttu-id="865f5-170">항목을 큐의 시작 부분에 다시 배치하는 순서는 보장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-170">The order in which the items are put back on the head of the queue is not guaranteed.</span></span> <span data-ttu-id="865f5-171">다음 코드를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-171">Let us look at the following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort the transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="865f5-172">다음과 같은 순서로 항목을 큐에서 제거한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-172">Assume that the items were dequeued in the following order:</span></span>
> <span data-ttu-id="865f5-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="865f5-173">10, 20</span></span>

<span data-ttu-id="865f5-174">트랜잭션을 중단하는 경우 항목은 다음 순서로 큐의 시작 부분에 다시 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-174">When we abort the transaction, the items would be added back to the head of the queue in any of the following orders:</span></span>
> <span data-ttu-id="865f5-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="865f5-175">10, 20</span></span>

> <span data-ttu-id="865f5-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="865f5-176">20, 10</span></span>

<span data-ttu-id="865f5-177">트랜잭션이 성공적으로 *커밋되지* 않은 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-177">The same is true for all cases where the transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="865f5-178">프로그래밍 패턴</span><span class="sxs-lookup"><span data-stu-id="865f5-178">Programming Patterns</span></span>
<span data-ttu-id="865f5-179">이 섹션에서는 ReliableConcurrentQueue를 사용하는 데 도움이 될 수 있는 몇 가지 프로그래밍 패턴을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="865f5-180">큐에서 제거 일괄 처리</span><span class="sxs-lookup"><span data-stu-id="865f5-180">Batch Dequeues</span></span>
<span data-ttu-id="865f5-181">한 번에 큐에서 제거를 수행하는 대신 큐에서 제거를 일괄 처리하는 소비자 작업의 경우 프로그래밍 패턴을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-181">A recommended programming pattern is for the consumer task to batch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="865f5-182">사용자는 모든 일괄 처리 또는 일괄 처리 크기 간에 지연 시간을 제한하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-182">The user can choose to throttle delays between every batch or the batch size.</span></span> <span data-ttu-id="865f5-183">다음 코드 조각에서는 이 프로그래밍 모델을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-183">The following code snippet shows this programming model.</span></span>  <span data-ttu-id="865f5-184">이 예제에서 트랜잭션이 커밋된 후에 처리를 수행합니다. 따라서 처리하는 동안 오류가 발생하는 경우 처리되지 않은 항목은 처리되지 않고 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-184">Note that in this example, the processing is done after the transaction is committed, so if a fault were to occur while processing, the unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="865f5-185">또는 트랜잭션 범위 내에서 처리를 수행할 수 있지만 그러면 성능에 부정적인 영향을 주고 이미 처리된 항목을 처리해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-185">Alternatively, the processing can be done within the transaction's scope, however this may have a negative impact on performance and requires handling of the items already processed.</span></span>

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break the for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="865f5-186">최상의 알림 기반 처리</span><span class="sxs-lookup"><span data-stu-id="865f5-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="865f5-187">개수 API를 사용하는 또 다른 프로그래밍 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-187">Another interesting programming pattern uses the Count API.</span></span> <span data-ttu-id="865f5-188">여기서는 큐에 대해 최상의 알림 기반 처리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-188">Here, we can implement best-effort notification-based processing for the queue.</span></span> <span data-ttu-id="865f5-189">큐 개수는 큐에 넣기 또는 큐에서 제거 작업을 제한하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-189">The queue Count can be used to throttle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="865f5-190">이전 예제와 같이 처리가 트랜잭션 외부에서 발생하므로 처리하는 동안 오류가 발생하는 경우 처리되지 않은 항목은 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-190">Note that as in the previous example, since the processing occurs outside the transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If the queue does not have the threshold number of items, delay the task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process the queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="865f5-191">최상의 드레이닝</span><span class="sxs-lookup"><span data-stu-id="865f5-191">Best-Effort Drain</span></span>
<span data-ttu-id="865f5-192">데이터 구조의 동시 특성으로 인해 큐의 드레이닝을 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-192">A drain of the queue cannot be guaranteed due to the concurrent nature of the data structure.</span></span>  <span data-ttu-id="865f5-193">큐에서 사용자 작업이 진행되지 않는 경우더라도 TryDequeueAsync에 대한 특정 호출은 이전에 큐에 넣고 커밋된 항목을 반환하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-193">It is possible that, even if no user operations on the queue are in-flight, a particular call to TryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="865f5-194">큐에 넣은 항목은 *결국* 큐에서 제거된다고 표시되지만 모든 생산자가 중지되고 새 큐에 넣기 작업이 허용되는 경우에도 독립 소비자는 대역외 통신 메커니즘 없이 큐가 안정적인 상태에 도달했음을 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-194">The enqueued item is guaranteed to *eventually* become visible to dequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that the queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="865f5-195">따라서 드레이닝 작업은 아래와 같이 구현될 때 가장 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-195">Thus, the drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="865f5-196">사용자는 큐를 비우기 전에 모든 추가 생산자와 소비자 작업을 중지하고 실행 중인 모든 트랜잭션을 커밋하거나 중단할 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-196">The user should stop all further producer and consumer tasks, and wait for any in-flight transactions to commit or abort, before attempting to drain the queue.</span></span>  <span data-ttu-id="865f5-197">사용자가 예상된 큐의 항목 수를 아는 경우 모든 항목이 큐에서 제거되었음을 알리는 알림을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-197">If the user knows the expected number of items in the queue, they can set up a notification which signals that all items have been dequeued.</span></span>

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer the dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="865f5-198">보기</span><span class="sxs-lookup"><span data-stu-id="865f5-198">Peek</span></span>
<span data-ttu-id="865f5-199">ReliableConcurrentQueue는 *TryPeekAsync* API를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-199">ReliableConcurrentQueue does not provide the *TryPeekAsync* api.</span></span> <span data-ttu-id="865f5-200">사용자는 *TryDequeueAsync*를 사용한 다음 트랜잭션을 중단하여 보기 의미 체계를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-200">Users can get the peek semantic by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="865f5-201">이 예제에서는 큐에서 제거는 항목의 값이 *10*보다 큰 경우에만 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="865f5-201">In this example, dequeues are processed only if the item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process the item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a><span data-ttu-id="865f5-202">필수 참고 목록</span><span class="sxs-lookup"><span data-stu-id="865f5-202">Must Read</span></span>
* [<span data-ttu-id="865f5-203">Reliable Services 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="865f5-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="865f5-204">신뢰할 수 있는 컬렉션 작업</span><span class="sxs-lookup"><span data-stu-id="865f5-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="865f5-205">Reliable Services 알림</span><span class="sxs-lookup"><span data-stu-id="865f5-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="865f5-206">Reliable Services 백업 및 복원(재해 복구)</span><span class="sxs-lookup"><span data-stu-id="865f5-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="865f5-207">신뢰할 수 있는 상태 관리자 구성</span><span class="sxs-lookup"><span data-stu-id="865f5-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="865f5-208">Service Fabric Web API 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="865f5-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="865f5-209">Reliable Services 프로그래밍 모델 고급 사용법</span><span class="sxs-lookup"><span data-stu-id="865f5-209">Advanced Usage of the Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="865f5-210">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="865f5-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
