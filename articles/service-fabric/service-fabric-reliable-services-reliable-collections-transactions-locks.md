---
title: "Azure 서비스 패브릭 신뢰할 수 있는 컬렉션의 잠금 모드와 aaaTransactions | Microsoft Docs"
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
ms.openlocfilehash: 340e029aa98f43ad6e46b48f687dad01f9d96f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a><span data-ttu-id="fb6cd-103">Azure Service Fabric 신뢰할 수 있는 컬렉션의 트랜잭션 및 잠금 모드</span><span class="sxs-lookup"><span data-stu-id="fb6cd-103">Transactions and lock modes in Azure Service Fabric Reliable Collections</span></span>

## <a name="transaction"></a><span data-ttu-id="fb6cd-104">트랜잭션</span><span class="sxs-lookup"><span data-stu-id="fb6cd-104">Transaction</span></span>
<span data-ttu-id="fb6cd-105">트랜잭션은 작업의 단일 논리적 단위로 수행되는 작업 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-105">A transaction is a sequence of operations performed as a single logical unit of work.</span></span>
<span data-ttu-id="fb6cd-106">트랜잭션이 다음 트랜잭션의 ACID 속성이 hello를 시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-106">A transaction must exhibit hello following ACID properties.</span></span> <span data-ttu-id="fb6cd-107">(참조: https://technet.microsoft.com/en-us/library/ms190612)</span><span class="sxs-lookup"><span data-stu-id="fb6cd-107">(see: https://technet.microsoft.com/en-us/library/ms190612)</span></span>
* <span data-ttu-id="fb6cd-108">**원자성**: 트랜잭션은 작업의 원자 단위여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-108">**Atomicity**: A transaction must be an atomic unit of work.</span></span> <span data-ttu-id="fb6cd-109">즉, 모든 데이터 수정 작업이 수행되거나, 또는 하나도 수행되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-109">In other words, either all its data modifications are performed, or none of them is performed.</span></span>
* <span data-ttu-id="fb6cd-110">**일관성**: 완료되면 트랜잭션은 모든 데이터를 일관된 상태로 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-110">**Consistency**: When completed, a transaction must leave all data in a consistent state.</span></span> <span data-ttu-id="fb6cd-111">모든 내부 데이터 구조는 hello hello 트랜잭션이 끝나기 전에 정확 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-111">All internal data structures must be correct at hello end of hello transaction.</span></span>
* <span data-ttu-id="fb6cd-112">**격리**: 수정한 동시 트랜잭션이 다른 동시 트랜잭션에 의해 hello 수정 되지 않도록에서 격리 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-112">**Isolation**: Modifications made by concurrent transactions must be isolated from hello modifications made by any other concurrent transactions.</span></span> <span data-ttu-id="fb6cd-113">ITransaction 내에서 작업에 사용 되는 hello 격리 수준은 hello IReliableState 수행 되는 hello 작업에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-113">hello isolation level used for an operation within an ITransaction is determined by hello IReliableState performing hello operation.</span></span>
* <span data-ttu-id="fb6cd-114">**내구성**: 트랜잭션이 완료 되 면 그 효과 영구적으로 준비에서 hello s입니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-114">**Durability**: After a transaction has completed, its effects are permanently in place in hello system.</span></span> <span data-ttu-id="fb6cd-115">hello 수정은 시스템 오류의 hello 이벤트에도 지속 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-115">hello modifications persist even in hello event of a system failure.</span></span>

### <a name="isolation-levels"></a><span data-ttu-id="fb6cd-116">격리 수준</span><span class="sxs-lookup"><span data-stu-id="fb6cd-116">Isolation levels</span></span>
<span data-ttu-id="fb6cd-117">Hello 정도 정의 하는 격리 수준을 toowhich hello 트랜잭션 다른 트랜잭션에 의해 수정 되지 않도록에서 격리 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-117">Isolation level defines hello degree toowhich hello transaction must be isolated from modifications made by other transactions.</span></span>
<span data-ttu-id="fb6cd-118">신뢰할 수 있는 컬렉션에서 지원되는 두 격리 수준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-118">There are two isolation levels that are supported in Reliable Collections:</span></span>

* <span data-ttu-id="fb6cd-119">**반복 읽기**: 문이 수정 되었지만 아직 커밋되지 않은 다른 트랜잭션에서 데이터를 읽을 수 없도록 하 고 다른 트랜잭션이 현재 hello까지 hello 현재 트랜잭션에서 읽은 데이터를 수정할 수 있는지를 지정 합니다. 트랜잭션을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-119">**Repeatable Read**: Specifies that statements cannot read data that has been modified but not yet committed by other transactions and that no other transactions can modify data that has been read by hello current transaction until hello current transaction finishes.</span></span> <span data-ttu-id="fb6cd-120">자세한 내용은 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-120">For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).</span></span>
* <span data-ttu-id="fb6cd-121">**스냅숏**: 트랜잭션의 모든 문에서 읽는 데이터 hello와 버전의 일관성이 hello hello 트랜잭션 시작 시 hello 데이터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-121">**Snapshot**: Specifies that data read by any statement in a transaction is hello transactionally consistent version of hello data that existed at hello start of hello transaction.</span></span>
  <span data-ttu-id="fb6cd-122">hello 트랜잭션 hello hello 트랜잭션이 시작 되기 전에 커밋된 데이터 수정 내용만 인식할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-122">hello transaction can recognize only data modifications that were committed before hello start of hello transaction.</span></span>
  <span data-ttu-id="fb6cd-123">Hello hello 현재 트랜잭션의 시작 이후 다른 트랜잭션에서 발생 수정한 데이터 표시 toostatements hello 현재 트랜잭션에서 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-123">Data modifications made by other transactions after hello start of hello current transaction are not visible toostatements executing in hello current transaction.</span></span>
  <span data-ttu-id="fb6cd-124">hello hello hello 트랜잭션 시작 당시 hello 문은 hello 커밋된 데이터의 스냅숏을 가져오는 처럼 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-124">hello effect is as if hello statements in a transaction get a snapshot of hello committed data as it existed at hello start of hello transaction.</span></span>
  <span data-ttu-id="fb6cd-125">스냅숏은 신뢰할 수 있는 컬렉션 간에 일관됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-125">Snapshots are consistent across Reliable Collections.</span></span>
  <span data-ttu-id="fb6cd-126">자세한 내용은 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-126">For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).</span></span>

<span data-ttu-id="fb6cd-127">신뢰할 수 있는 컬렉션 hello 트랜잭션의 생성 시 hello 작업과 hello 복제본의 hello 역할에 따라 지정 된 읽기 작업이 격리 수준 toouse hello를 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-127">Reliable Collections automatically choose hello isolation level toouse for a given read operation depending on hello operation and hello role of hello replica at hello time of transaction's creation.</span></span>
<span data-ttu-id="fb6cd-128">다음은 신뢰할 수 있는 사전 및 큐 작업에 대 한 격리 수준 기본값을 보여 주는 hello 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-128">Following is hello table that depicts isolation level defaults for Reliable Dictionary and Queue operations.</span></span>

| <span data-ttu-id="fb6cd-129">작업 \ 역할</span><span class="sxs-lookup"><span data-stu-id="fb6cd-129">Operation \ Role</span></span> | <span data-ttu-id="fb6cd-130">보조</span><span class="sxs-lookup"><span data-stu-id="fb6cd-130">Primary</span></span> | <span data-ttu-id="fb6cd-131">주</span><span class="sxs-lookup"><span data-stu-id="fb6cd-131">Secondary</span></span> |
| --- |:--- |:--- |
| <span data-ttu-id="fb6cd-132">단일 엔터티 읽기</span><span class="sxs-lookup"><span data-stu-id="fb6cd-132">Single Entity Read</span></span> |<span data-ttu-id="fb6cd-133">반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="fb6cd-133">Repeatable Read</span></span> |<span data-ttu-id="fb6cd-134">스냅숏</span><span class="sxs-lookup"><span data-stu-id="fb6cd-134">Snapshot</span></span> |
| <span data-ttu-id="fb6cd-135">열거형, 개수</span><span class="sxs-lookup"><span data-stu-id="fb6cd-135">Enumeration, Count</span></span> |<span data-ttu-id="fb6cd-136">스냅숏</span><span class="sxs-lookup"><span data-stu-id="fb6cd-136">Snapshot</span></span> |<span data-ttu-id="fb6cd-137">스냅숏</span><span class="sxs-lookup"><span data-stu-id="fb6cd-137">Snapshot</span></span> |

> [!NOTE]
> <span data-ttu-id="fb6cd-138">단일 엔터티 작업에 대한 일반적인 예제는 `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`입니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-138">Common examples for Single Entity Operations are `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`.</span></span>
> 

<span data-ttu-id="fb6cd-139">신뢰할 수 있는 사전 hello와 hello 신뢰할 수 있는 큐 읽기 Your 작성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-139">Both hello Reliable Dictionary and hello Reliable Queue support Read Your Writes.</span></span>
<span data-ttu-id="fb6cd-140">트랜잭션 내에서 표시 tooa 다음 읽을 toohello 속하는 쓰기 즉, 동일한 트랜잭션.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-140">In other words, any write within a transaction will be visible tooa following read that belongs toohello same transaction.</span></span>

## <a name="locks"></a><span data-ttu-id="fb6cd-141">잠금</span><span class="sxs-lookup"><span data-stu-id="fb6cd-141">Locks</span></span>
<span data-ttu-id="fb6cd-142">신뢰할 수 있는 컬렉션에서 모든 트랜잭션을 구현 엄격한 2 단계 잠금: 트랜잭션 중단 또는 커밋 hello 트랜잭션이 종료 될 때까지 확보 한 hello 잠금 해제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-142">In Reliable Collections, all transactions implement rigorous two phase locking: a transaction does not release hello locks it has acquired until hello transaction terminates with either an abort or a commit.</span></span>

<span data-ttu-id="fb6cd-143">신뢰할 수 있는 사전은 모든 단일 엔터티 작업에 대해 행 수준 잠금을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-143">Reliable Dictionary uses row level locking for all single entity operations.</span></span>
<span data-ttu-id="fb6cd-144">신뢰할 수 있는 큐와 엄격한 트랜잭션 FIFO 속성의 동시성은 서로 균형을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-144">Reliable Queue trades off concurrency for strict transactional FIFO property.</span></span>
<span data-ttu-id="fb6cd-145">신뢰할 수 있는 큐는 작업 수준 잠금을 사용하여 한 번에 한 트랜잭션에는 `TryPeekAsync` 및/또는 `TryDequeueAsync`를 허용하고, 다른 트랜잭션에는 `EnqueueAsync`를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-145">Reliable Queue uses operation level locks allowing one transaction with `TryPeekAsync` and/or `TryDequeueAsync` and one transaction with `EnqueueAsync` at a time.</span></span>
<span data-ttu-id="fb6cd-146">참고 해당 toopreserve FIFO, 경우에 `TryPeekAsync` 또는 `TryDequeueAsync` hello 신뢰할 수 있는 큐가 비어, 또한 잠급니다 적이 관찰 `EnqueueAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-146">Note that toopreserve FIFO, if a `TryPeekAsync` or `TryDequeueAsync` ever observes that hello Reliable Queue is empty, they will also lock `EnqueueAsync`.</span></span>

<span data-ttu-id="fb6cd-147">쓰기 작업은 항상 배타적 잠금을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-147">Write operations always take Exclusive locks.</span></span>
<span data-ttu-id="fb6cd-148">읽기 작업 hello 잠금에 여러 요인에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-148">For read operations, hello locking depends on a couple of factors.</span></span>
<span data-ttu-id="fb6cd-149">스냅숏 격리를 사용하여 수행된 모든 읽기 작업은 잠금이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-149">Any read operation done using Snapshot isolation is lock free.</span></span>
<span data-ttu-id="fb6cd-150">모든 반복 가능한 읽기 작업은 기본적으로 공유 잠금을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-150">Any Repeatable Read operation by default takes Shared locks.</span></span>
<span data-ttu-id="fb6cd-151">그러나 반복 가능한 읽기를 지 원하는 모든 읽기 작업, hello 사용자 hello 공유 잠금 대신 업데이트 잠금에 대 한 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-151">However, for any read operation that supports Repeatable Read, hello user can ask for an Update lock instead of hello Shared lock.</span></span>
<span data-ttu-id="fb6cd-152">업데이트 잠금은 비대칭 잠금 tooprevent 일반적인 형태의 교착 상태 여러 트랜잭션을 나중에 업데이트에 대 한 리소스를 잠글 때 발생 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-152">An Update lock is an asymmetric lock used tooprevent a common form of deadlock that occurs when multiple transactions lock resources for potential updates at a later time.</span></span>

<span data-ttu-id="fb6cd-153">다음 표에 hello에 hello 잠금 호환성 표를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-153">hello lock compatibility matrix can be found in hello following table:</span></span>

| <span data-ttu-id="fb6cd-154">요청 \ 부여</span><span class="sxs-lookup"><span data-stu-id="fb6cd-154">Request \ Granted</span></span> | <span data-ttu-id="fb6cd-155">없음</span><span class="sxs-lookup"><span data-stu-id="fb6cd-155">None</span></span> | <span data-ttu-id="fb6cd-156">공유됨</span><span class="sxs-lookup"><span data-stu-id="fb6cd-156">Shared</span></span> | <span data-ttu-id="fb6cd-157">업데이트</span><span class="sxs-lookup"><span data-stu-id="fb6cd-157">Update</span></span> | <span data-ttu-id="fb6cd-158">단독</span><span class="sxs-lookup"><span data-stu-id="fb6cd-158">Exclusive</span></span> |
| --- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="fb6cd-159">공유됨</span><span class="sxs-lookup"><span data-stu-id="fb6cd-159">Shared</span></span> |<span data-ttu-id="fb6cd-160">충돌 없음</span><span class="sxs-lookup"><span data-stu-id="fb6cd-160">No conflict</span></span> |<span data-ttu-id="fb6cd-161">충돌 없음</span><span class="sxs-lookup"><span data-stu-id="fb6cd-161">No conflict</span></span> |<span data-ttu-id="fb6cd-162">충돌</span><span class="sxs-lookup"><span data-stu-id="fb6cd-162">Conflict</span></span> |<span data-ttu-id="fb6cd-163">충돌</span><span class="sxs-lookup"><span data-stu-id="fb6cd-163">Conflict</span></span> |
| <span data-ttu-id="fb6cd-164">업데이트</span><span class="sxs-lookup"><span data-stu-id="fb6cd-164">Update</span></span> |<span data-ttu-id="fb6cd-165">충돌 없음</span><span class="sxs-lookup"><span data-stu-id="fb6cd-165">No conflict</span></span> |<span data-ttu-id="fb6cd-166">충돌 없음</span><span class="sxs-lookup"><span data-stu-id="fb6cd-166">No conflict</span></span> |<span data-ttu-id="fb6cd-167">충돌</span><span class="sxs-lookup"><span data-stu-id="fb6cd-167">Conflict</span></span> |<span data-ttu-id="fb6cd-168">충돌</span><span class="sxs-lookup"><span data-stu-id="fb6cd-168">Conflict</span></span> |
| <span data-ttu-id="fb6cd-169">단독</span><span class="sxs-lookup"><span data-stu-id="fb6cd-169">Exclusive</span></span> |<span data-ttu-id="fb6cd-170">충돌 없음</span><span class="sxs-lookup"><span data-stu-id="fb6cd-170">No conflict</span></span> |<span data-ttu-id="fb6cd-171">충돌</span><span class="sxs-lookup"><span data-stu-id="fb6cd-171">Conflict</span></span> |<span data-ttu-id="fb6cd-172">충돌</span><span class="sxs-lookup"><span data-stu-id="fb6cd-172">Conflict</span></span> |<span data-ttu-id="fb6cd-173">충돌</span><span class="sxs-lookup"><span data-stu-id="fb6cd-173">Conflict</span></span> |

<span data-ttu-id="fb6cd-174">제한 시간 인수가 hello 신뢰할 수 있는 컬렉션 Api에서에서 교착 상태 감지에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-174">Time-out argument in hello Reliable Collections APIs is used for deadlock detection.</span></span>
<span data-ttu-id="fb6cd-175">예를 들어 두 개의 트랜잭션 (t 1과 T2) tooread 시도 하 고 K1를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-175">For example, two transactions (T1 and T2) are trying tooread and update K1.</span></span>
<span data-ttu-id="fb6cd-176">공유할 수는 toodeadlock, 결국 모두 때문에 잠금 공유 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-176">It is possible for them toodeadlock, because they both end up having hello Shared lock.</span></span>
<span data-ttu-id="fb6cd-177">이 경우 하나 또는 둘 다 hello 작업 시간이 초과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-177">In this case, one or both of hello operations will time out.</span></span>

<span data-ttu-id="fb6cd-178">이 교착 상태 시나리오는 업데이트 잠금이 교착 상태를 방지하는 방법을 보여주는 좋은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="fb6cd-178">This deadlock scenario is a great example of how an Update lock can prevent deadlocks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb6cd-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fb6cd-179">Next steps</span></span>
* [<span data-ttu-id="fb6cd-180">신뢰할 수 있는 컬렉션 작업</span><span class="sxs-lookup"><span data-stu-id="fb6cd-180">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="fb6cd-181">Reliable Services 알림</span><span class="sxs-lookup"><span data-stu-id="fb6cd-181">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="fb6cd-182">Reliable Services 백업 및 복원(재해 복구)</span><span class="sxs-lookup"><span data-stu-id="fb6cd-182">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="fb6cd-183">신뢰할 수 있는 상태 관리자 구성</span><span class="sxs-lookup"><span data-stu-id="fb6cd-183">Reliable State Manager configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="fb6cd-184">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="fb6cd-184">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

