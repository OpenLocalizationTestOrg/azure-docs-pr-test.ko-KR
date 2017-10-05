---
title: "Azure Service Fabric 신뢰할 수 있는 컬렉션의 트랜잭션 및 잠금 모드 | Microsoft Docs"
description: "Azure Service Fabric 신뢰할 수 있는 상태 관리자 및 신뢰할 수 있는 컬렉션 트랜잭션 및 잠금."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 3452473f5b2f86d29e46339c997193bc6403736a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a><span data-ttu-id="c5712-103">Azure Service Fabric 신뢰할 수 있는 컬렉션의 트랜잭션 및 잠금 모드</span><span class="sxs-lookup"><span data-stu-id="c5712-103">Transactions and lock modes in Azure Service Fabric Reliable Collections</span></span>

## <a name="transaction"></a><span data-ttu-id="c5712-104">트랜잭션</span><span class="sxs-lookup"><span data-stu-id="c5712-104">Transaction</span></span>
<span data-ttu-id="c5712-105">트랜잭션은 작업의 단일 논리적 단위로 수행되는 작업 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-105">A transaction is a sequence of operations performed as a single logical unit of work.</span></span>
<span data-ttu-id="c5712-106">트랜잭션은 다음 ACID 속성을 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-106">A transaction must exhibit the following ACID properties.</span></span> <span data-ttu-id="c5712-107">(참조: https://technet.microsoft.com/en-us/library/ms190612)</span><span class="sxs-lookup"><span data-stu-id="c5712-107">(see: https://technet.microsoft.com/en-us/library/ms190612)</span></span>
* <span data-ttu-id="c5712-108">**원자성**: 트랜잭션은 작업의 원자 단위여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-108">**Atomicity**: A transaction must be an atomic unit of work.</span></span> <span data-ttu-id="c5712-109">즉, 모든 데이터 수정 작업이 수행되거나, 또는 하나도 수행되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-109">In other words, either all its data modifications are performed, or none of them is performed.</span></span>
* <span data-ttu-id="c5712-110">**일관성**: 완료되면 트랜잭션은 모든 데이터를 일관된 상태로 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-110">**Consistency**: When completed, a transaction must leave all data in a consistent state.</span></span> <span data-ttu-id="c5712-111">모든 내부 데이터 구조는 트랜잭션이 끝날 때 정확해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-111">All internal data structures must be correct at the end of the transaction.</span></span>
* <span data-ttu-id="c5712-112">**격리**: 동시 트랜잭션에 의한 수정은 다른 동시 트랜잭션과 격리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-112">**Isolation**: Modifications made by concurrent transactions must be isolated from the modifications made by any other concurrent transactions.</span></span> <span data-ttu-id="c5712-113">ITransaction 내에서 작업에 사용되는 격리 수준은 작업을 수행하는 IReliableState에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-113">The isolation level used for an operation within an ITransaction is determined by the IReliableState performing the operation.</span></span>
* <span data-ttu-id="c5712-114">**내구성**: 트랜잭션이 완료되면 그 영향은 영구적으로 시스템에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-114">**Durability**: After a transaction has completed, its effects are permanently in place in the system.</span></span> <span data-ttu-id="c5712-115">수정은 시스템 오류가 발생하는 경우에도 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-115">The modifications persist even in the event of a system failure.</span></span>

### <a name="isolation-levels"></a><span data-ttu-id="c5712-116">격리 수준</span><span class="sxs-lookup"><span data-stu-id="c5712-116">Isolation levels</span></span>
<span data-ttu-id="c5712-117">격리 수준은 트랜잭션은 다른 트랜잭션에 의해 수정되지 않도록 격리해야 하는 정도를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-117">Isolation level defines the degree to which the transaction must be isolated from modifications made by other transactions.</span></span>
<span data-ttu-id="c5712-118">신뢰할 수 있는 컬렉션에서 지원되는 두 격리 수준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-118">There are two isolation levels that are supported in Reliable Collections:</span></span>

* <span data-ttu-id="c5712-119">**반복 가능한 읽기**: 문은 수정되었지만 다른 트랜잭션에서 아직 커밋되지 않은 데이터를 읽을 수 없으며 현재 트랜잭션이 완료될 때까지 다른 트랜잭션은 현재 트랜잭션에서 읽은 데이터를 수정할 수 없음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-119">**Repeatable Read**: Specifies that statements cannot read data that has been modified but not yet committed by other transactions and that no other transactions can modify data that has been read by the current transaction until the current transaction finishes.</span></span> <span data-ttu-id="c5712-120">자세한 내용은 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5712-120">For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).</span></span>
* <span data-ttu-id="c5712-121">**스냅숏**: 트랜잭션의 문에서 읽은 데이터가 트랜잭션 시작 부분에 존재하는 데이터의 트랜잭션이 일치되는 버전이 되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-121">**Snapshot**: Specifies that data read by any statement in a transaction is the transactionally consistent version of the data that existed at the start of the transaction.</span></span>
  <span data-ttu-id="c5712-122">트랜잭션은 트랜잭션 시작 전에 커밋된 데이터 수정 내용만 인식할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-122">The transaction can recognize only data modifications that were committed before the start of the transaction.</span></span>
  <span data-ttu-id="c5712-123">현재 트랜잭션이 시작된 후 다른 트랜잭션에서 수행한 데이터 수정 내용은 현재 트랜잭션에서 실행 중인 문에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-123">Data modifications made by other transactions after the start of the current transaction are not visible to statements executing in the current transaction.</span></span>
  <span data-ttu-id="c5712-124">그 결과 트랜잭션의 문이 트랜잭션 시작 당시 커밋된 데이터의 스냅숏을 가져오는 것처럼 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-124">The effect is as if the statements in a transaction get a snapshot of the committed data as it existed at the start of the transaction.</span></span>
  <span data-ttu-id="c5712-125">스냅숏은 신뢰할 수 있는 컬렉션 간에 일관됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-125">Snapshots are consistent across Reliable Collections.</span></span>
  <span data-ttu-id="c5712-126">자세한 내용은 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5712-126">For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).</span></span>

<span data-ttu-id="c5712-127">신뢰할 수 있는 컬렉션은 트랜잭션을 만들 당시의 작업 및 복제본의 역할에 따라 자동으로 특정 읽기 작업에 사용할 격리 수준을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-127">Reliable Collections automatically choose the isolation level to use for a given read operation depending on the operation and the role of the replica at the time of transaction's creation.</span></span>
<span data-ttu-id="c5712-128">다음 테이블에는 신뢰할 수 있는 사전 및 큐 작업에 대한 기본 격리 수준이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-128">Following is the table that depicts isolation level defaults for Reliable Dictionary and Queue operations.</span></span>

| <span data-ttu-id="c5712-129">작업 \ 역할</span><span class="sxs-lookup"><span data-stu-id="c5712-129">Operation \ Role</span></span> | <span data-ttu-id="c5712-130">보조</span><span class="sxs-lookup"><span data-stu-id="c5712-130">Primary</span></span> | <span data-ttu-id="c5712-131">주</span><span class="sxs-lookup"><span data-stu-id="c5712-131">Secondary</span></span> |
| --- |:--- |:--- |
| <span data-ttu-id="c5712-132">단일 엔터티 읽기</span><span class="sxs-lookup"><span data-stu-id="c5712-132">Single Entity Read</span></span> |<span data-ttu-id="c5712-133">반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="c5712-133">Repeatable Read</span></span> |<span data-ttu-id="c5712-134">스냅숏</span><span class="sxs-lookup"><span data-stu-id="c5712-134">Snapshot</span></span> |
| <span data-ttu-id="c5712-135">열거형, 개수</span><span class="sxs-lookup"><span data-stu-id="c5712-135">Enumeration, Count</span></span> |<span data-ttu-id="c5712-136">스냅숏</span><span class="sxs-lookup"><span data-stu-id="c5712-136">Snapshot</span></span> |<span data-ttu-id="c5712-137">스냅숏</span><span class="sxs-lookup"><span data-stu-id="c5712-137">Snapshot</span></span> |

> [!NOTE]
> <span data-ttu-id="c5712-138">단일 엔터티 작업에 대한 일반적인 예제는 `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`입니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-138">Common examples for Single Entity Operations are `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`.</span></span>
> 

<span data-ttu-id="c5712-139">신뢰할 수 있는 사전 및 신뢰할 수 있는 큐는 모두 읽기 프로그램 작성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-139">Both the Reliable Dictionary and the Reliable Queue support Read Your Writes.</span></span>
<span data-ttu-id="c5712-140">즉, 특정 트랜잭션 내 모든 쓰기가 동일한 트랜잭션에 속하는 다음 읽기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-140">In other words, any write within a transaction will be visible to a following read that belongs to the same transaction.</span></span>

## <a name="locks"></a><span data-ttu-id="c5712-141">잠금</span><span class="sxs-lookup"><span data-stu-id="c5712-141">Locks</span></span>
<span data-ttu-id="c5712-142">신뢰할 수 있는 컬렉션의 모든 트랜잭션은 엄격한 2단계 잠금을 구현합니다. 트랜잭션은 중단 또는 커밋으로 인해 종료되어야만 확보한 잠금을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-142">In Reliable Collections, all transactions implement rigorous two phase locking: a transaction does not release the locks it has acquired until the transaction terminates with either an abort or a commit.</span></span>

<span data-ttu-id="c5712-143">신뢰할 수 있는 사전은 모든 단일 엔터티 작업에 대해 행 수준 잠금을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-143">Reliable Dictionary uses row level locking for all single entity operations.</span></span>
<span data-ttu-id="c5712-144">신뢰할 수 있는 큐와 엄격한 트랜잭션 FIFO 속성의 동시성은 서로 균형을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-144">Reliable Queue trades off concurrency for strict transactional FIFO property.</span></span>
<span data-ttu-id="c5712-145">신뢰할 수 있는 큐는 작업 수준 잠금을 사용하여 한 번에 한 트랜잭션에는 `TryPeekAsync` 및/또는 `TryDequeueAsync`를 허용하고, 다른 트랜잭션에는 `EnqueueAsync`를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-145">Reliable Queue uses operation level locks allowing one transaction with `TryPeekAsync` and/or `TryDequeueAsync` and one transaction with `EnqueueAsync` at a time.</span></span>
<span data-ttu-id="c5712-146">FIFO를 유지하기 위해 `TryPeekAsync` 또는 `TryDequeueAsync`는 신뢰할 수 있는 큐가 비어 있음을 확인하면 `EnqueueAsync`도 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-146">Note that to preserve FIFO, if a `TryPeekAsync` or `TryDequeueAsync` ever observes that the Reliable Queue is empty, they will also lock `EnqueueAsync`.</span></span>

<span data-ttu-id="c5712-147">쓰기 작업은 항상 배타적 잠금을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-147">Write operations always take Exclusive locks.</span></span>
<span data-ttu-id="c5712-148">읽기 작업의 경우 몇 가지 요인에 따라 잠금이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-148">For read operations, the locking depends on a couple of factors.</span></span>
<span data-ttu-id="c5712-149">스냅숏 격리를 사용하여 수행된 모든 읽기 작업은 잠금이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-149">Any read operation done using Snapshot isolation is lock free.</span></span>
<span data-ttu-id="c5712-150">모든 반복 가능한 읽기 작업은 기본적으로 공유 잠금을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-150">Any Repeatable Read operation by default takes Shared locks.</span></span>
<span data-ttu-id="c5712-151">그러나 사용자는 반복 가능한 읽기를 지원하는 모든 읽기 작업에 대해 공유 잠금 대신 업데이트 잠금을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-151">However, for any read operation that supports Repeatable Read, the user can ask for an Update lock instead of the Shared lock.</span></span>
<span data-ttu-id="c5712-152">업데이트 잠금에는 이후의 잠재적 업데이트를 위해 여러 트랜잭션이 리소스를 잠글 때 발생하는 일반적인 형태의 교착 상태를 방지하는 데 사용되는 비대칭 잠금입니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-152">An Update lock is an asymmetric lock used to prevent a common form of deadlock that occurs when multiple transactions lock resources for potential updates at a later time.</span></span>

<span data-ttu-id="c5712-153">잠금 호환성 매트릭스는 다음 테이블에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-153">The lock compatibility matrix can be found in the following table:</span></span>

| <span data-ttu-id="c5712-154">요청 \ 부여</span><span class="sxs-lookup"><span data-stu-id="c5712-154">Request \ Granted</span></span> | <span data-ttu-id="c5712-155">없음</span><span class="sxs-lookup"><span data-stu-id="c5712-155">None</span></span> | <span data-ttu-id="c5712-156">공유됨</span><span class="sxs-lookup"><span data-stu-id="c5712-156">Shared</span></span> | <span data-ttu-id="c5712-157">업데이트</span><span class="sxs-lookup"><span data-stu-id="c5712-157">Update</span></span> | <span data-ttu-id="c5712-158">단독</span><span class="sxs-lookup"><span data-stu-id="c5712-158">Exclusive</span></span> |
| --- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5712-159">공유됨</span><span class="sxs-lookup"><span data-stu-id="c5712-159">Shared</span></span> |<span data-ttu-id="c5712-160">충돌 없음</span><span class="sxs-lookup"><span data-stu-id="c5712-160">No conflict</span></span> |<span data-ttu-id="c5712-161">충돌 없음</span><span class="sxs-lookup"><span data-stu-id="c5712-161">No conflict</span></span> |<span data-ttu-id="c5712-162">충돌</span><span class="sxs-lookup"><span data-stu-id="c5712-162">Conflict</span></span> |<span data-ttu-id="c5712-163">충돌</span><span class="sxs-lookup"><span data-stu-id="c5712-163">Conflict</span></span> |
| <span data-ttu-id="c5712-164">업데이트</span><span class="sxs-lookup"><span data-stu-id="c5712-164">Update</span></span> |<span data-ttu-id="c5712-165">충돌 없음</span><span class="sxs-lookup"><span data-stu-id="c5712-165">No conflict</span></span> |<span data-ttu-id="c5712-166">충돌 없음</span><span class="sxs-lookup"><span data-stu-id="c5712-166">No conflict</span></span> |<span data-ttu-id="c5712-167">충돌</span><span class="sxs-lookup"><span data-stu-id="c5712-167">Conflict</span></span> |<span data-ttu-id="c5712-168">충돌</span><span class="sxs-lookup"><span data-stu-id="c5712-168">Conflict</span></span> |
| <span data-ttu-id="c5712-169">단독</span><span class="sxs-lookup"><span data-stu-id="c5712-169">Exclusive</span></span> |<span data-ttu-id="c5712-170">충돌 없음</span><span class="sxs-lookup"><span data-stu-id="c5712-170">No conflict</span></span> |<span data-ttu-id="c5712-171">충돌</span><span class="sxs-lookup"><span data-stu-id="c5712-171">Conflict</span></span> |<span data-ttu-id="c5712-172">충돌</span><span class="sxs-lookup"><span data-stu-id="c5712-172">Conflict</span></span> |<span data-ttu-id="c5712-173">충돌</span><span class="sxs-lookup"><span data-stu-id="c5712-173">Conflict</span></span> |

<span data-ttu-id="c5712-174">신뢰할 수 있는 컬렉션 API의 시간 제한 인수는 교착 상태 감지를 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-174">Time-out argument in the Reliable Collections APIs is used for deadlock detection.</span></span>
<span data-ttu-id="c5712-175">예를 들어 두 트랜잭션(T1과 T2)은 K1을 읽고 업데이트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-175">For example, two transactions (T1 and T2) are trying to read and update K1.</span></span>
<span data-ttu-id="c5712-176">둘 다 결국 공유된 잠금을 가지게 되기 때문에 교착 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-176">It is possible for them to deadlock, because they both end up having the Shared lock.</span></span>
<span data-ttu-id="c5712-177">이 경우 하나 또는 두 작업이 시간 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-177">In this case, one or both of the operations will time out.</span></span>

<span data-ttu-id="c5712-178">이 교착 상태 시나리오는 업데이트 잠금이 교착 상태를 방지하는 방법을 보여주는 좋은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c5712-178">This deadlock scenario is a great example of how an Update lock can prevent deadlocks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5712-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5712-179">Next steps</span></span>
* [<span data-ttu-id="c5712-180">신뢰할 수 있는 컬렉션 작업</span><span class="sxs-lookup"><span data-stu-id="c5712-180">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="c5712-181">Reliable Services 알림</span><span class="sxs-lookup"><span data-stu-id="c5712-181">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="c5712-182">Reliable Services 백업 및 복원(재해 복구)</span><span class="sxs-lookup"><span data-stu-id="c5712-182">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="c5712-183">신뢰할 수 있는 상태 관리자 구성</span><span class="sxs-lookup"><span data-stu-id="c5712-183">Reliable State Manager configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="c5712-184">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="c5712-184">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

