---
title: "Reliable Services 알림 | Microsoft Docs"
description: "서비스 패브릭 Reliable Services 알림에 대한 개념 설명서"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: c6a53d851510ed5e6eec1f3ac0f636ad034a6d4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="bdabd-103">Reliable Services 알림</span><span class="sxs-lookup"><span data-stu-id="bdabd-103">Reliable Services notifications</span></span>
<span data-ttu-id="bdabd-104">알림을 사용하면 클라이언트에서 관심 있는 개체에 대한 변경 내용을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-104">Notifications allow clients to track the changes that are being made to an object that they're interested in.</span></span> <span data-ttu-id="bdabd-105">*신뢰할 수 있는 상태 관리자* 및 *신뢰할 수 있는 사전*의 두 가지 개체 유형에서 알림을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="bdabd-106">알림을 사용하는 일반적인 이유:</span><span class="sxs-lookup"><span data-stu-id="bdabd-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="bdabd-107">보조 인덱스 또는 복제본 상태에 대한 집계된 필터링 보기와 같은 구체화된 보기를 구축하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-107">Building materialized views, such as secondary indexes or aggregated filtered views of the replica's state.</span></span> <span data-ttu-id="bdabd-108">신뢰할 수 있는 사전에 있는 모든 키의 정렬된 인덱스가 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="bdabd-109">지난 1시간 동안 추가된 사용자 수와 같은 모니터링 데이터를 전송하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-109">Sending monitoring data, such as the number of users added in the last hour.</span></span>

<span data-ttu-id="bdabd-110">알림은 작업 적용의 일부로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="bdabd-111">이 때문에 알림은 가능한 한 빨리 처리되어야 하며 동기 이벤트는 광범위한 작업을 포함하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="bdabd-112">신뢰할 수 있는 상태 관리자 알림</span><span class="sxs-lookup"><span data-stu-id="bdabd-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="bdabd-113">신뢰할 수 있는 상태 관리자는 다음 이벤트에 대한 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-113">Reliable State Manager provides notifications for the following events:</span></span>

* <span data-ttu-id="bdabd-114">트랜잭션</span><span class="sxs-lookup"><span data-stu-id="bdabd-114">Transaction</span></span>
  * <span data-ttu-id="bdabd-115">커밋</span><span class="sxs-lookup"><span data-stu-id="bdabd-115">Commit</span></span>
* <span data-ttu-id="bdabd-116">상태 관리자</span><span class="sxs-lookup"><span data-stu-id="bdabd-116">State manager</span></span>
  * <span data-ttu-id="bdabd-117">다시 빌드</span><span class="sxs-lookup"><span data-stu-id="bdabd-117">Rebuild</span></span>
  * <span data-ttu-id="bdabd-118">신뢰할 수 있는 상태 추가</span><span class="sxs-lookup"><span data-stu-id="bdabd-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="bdabd-119">신뢰할 수 있는 상태 제거</span><span class="sxs-lookup"><span data-stu-id="bdabd-119">Removal of a reliable state</span></span>

<span data-ttu-id="bdabd-120">신뢰할 수 있는 상태 관리자는 현재 처리 중인 트랜잭션을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-120">Reliable State Manager tracks the current inflight transactions.</span></span> <span data-ttu-id="bdabd-121">알림이 실행되도록 하는 유일한 트랜잭션 상태 변경은 커밋 중인 트랜잭션입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-121">The only change in transaction state that causes a notification to be fired is a transaction being committed.</span></span>

<span data-ttu-id="bdabd-122">신뢰할 수 있는 상태 관리자는 신뢰할 수 있는 사전 및 신뢰할 수 있는 큐와 같은 신뢰할 수 있는 상태 컬렉션을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="bdabd-123">신뢰할 수 있는 상태 관리자는 이 컬렉션이 변경될 때, 즉 신뢰할 수 있는 상태가 추가 또는 제거되거나 전체 컬렉션이 다시 작성될 때 알림을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or the entire collection is rebuilt.</span></span>
<span data-ttu-id="bdabd-124">신뢰할 수 있는 상태 관리자 컬렉션은 다음 세 가지 경우에 다시 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-124">The Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="bdabd-125">복구: 복제본이 시작되면 디스크에서 이전 상태를 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-125">Recovery: When a replica starts, it recovers its previous state from the disk.</span></span> <span data-ttu-id="bdabd-126">복구가 끝나면 **NotifyStateManagerChangedEventArgs** 를 사용하여 복구된 신뢰할 수 있는 상태 집합이 포함된 이벤트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-126">At the end of recovery, it uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of recovered reliable states.</span></span>
* <span data-ttu-id="bdabd-127">전체 복사: 복제본을 구성 집합에 포함하려면 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-127">Full copy: Before a replica can join the configuration set, it has to be built.</span></span> <span data-ttu-id="bdabd-128">경우에 따라 주 복제본의 신뢰할 수 있는 상태 관리자 상태의 전체 복사본을 유휴 보조 복제본에 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-128">Sometimes, this requires a full copy of Reliable State Manager's state from the primary replica to be applied to the idle secondary replica.</span></span> <span data-ttu-id="bdabd-129">보조 복제본의 신뢰할 수 있는 상태 관리자는 **NotifyStateManagerChangedEventArgs** 를 사용하여 주 복제본에서 획득한 신뢰할 수 있는 상태 집합이 포함된 이벤트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-129">Reliable State Manager on the secondary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it acquired from the primary replica.</span></span>
* <span data-ttu-id="bdabd-130">복원: 재해 복구 시나리오에서 **RestoreAsync**를 사용하여 백업에서 복제본의 상태를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-130">Restore: In disaster recovery scenarios, the replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="bdabd-131">이러한 경우 주 복제본의 신뢰할 수 있는 상태 관리자는 **NotifyStateManagerChangedEventArgs** 를 사용하여 백업에서 복원한 신뢰할 수 있는 상태 집합이 포함된 이벤트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-131">In such cases, Reliable State Manager on the primary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it restored from the backup.</span></span>

<span data-ttu-id="bdabd-132">트랜잭션 알림 및/또는 상태 관리자 알림을 등록하려면 신뢰할 수 있는 상태 관리자의 **TransactionChanged** 또는 **StateManagerChanged** 이벤트에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-132">To register for transaction notifications and/or state manager notifications, you need to register with the **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="bdabd-133">이러한 이벤트 처리기에 등록하는 일반적인 위치는 상태 저장 서비스의 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-133">A common place to register with these event handlers is the constructor of your stateful service.</span></span> <span data-ttu-id="bdabd-134">생성자에 등록하면 **IReliableStateManager**의 수명 동안 변경 내용으로 발생되는 모든 알림을 놓치지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-134">When you register on the constructor, you won't miss any notification that's caused by a change during the lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="bdabd-135">**TransactionChanged** 이벤트 처리기는 **NotifyTransactionChangedEventArgs**를 사용하여 이벤트에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-135">The **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** to provide details about the event.</span></span> <span data-ttu-id="bdabd-136">변경 유형을 지정하는 작업 속성(예: **NotifyTransactionChangedAction.Commit**)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-136">It contains the action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies the type of change.</span></span> <span data-ttu-id="bdabd-137">또한 변경된 트랜잭션에 대한 참조를 제공하는 트랜잭션 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-137">It also contains the transaction property that provides a reference to the transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="bdabd-138">오늘날 **TransactionChanged** 이벤트는 트랜잭션이 커밋되는 경우에만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-138">Today, **TransactionChanged** events are raised only if the transaction is committed.</span></span> <span data-ttu-id="bdabd-139">작업은 **NotifyTransactionChangedAction.Commit**와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-139">The action is then equal to **NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="bdabd-140">하지만 나중에 다른 유형의 트랜잭션 상태 변경에 대해 이벤트가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-140">But in the future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="bdabd-141">작업을 확인하고, 예상되는 작업인 경우에만 이벤트를 처리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-141">We recommend checking the action and processing the event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="bdabd-142">다음은 예제 **TransactionChanged** 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-142">Following is an example **TransactionChanged** event handler.</span></span>

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

<span data-ttu-id="bdabd-143">**StateManagerChanged** 이벤트 처리기는 **NotifyStateManagerChangedEventArgs**를 사용하여 이벤트에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-143">The **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="bdabd-144">**NotifyStateManagerChangedEventArgs**에는 두 가지 하위 클래스인 **NotifyStateManagerRebuildEventArgs**와 **NotifyStateManagerSingleEntityChangedEventArgs**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="bdabd-145">**NotifyStateManagerChangedEventArgs**의 작업 속성을 사용하여 **NotifyStateManagerChangedEventArgs**를 올바른 하위 클래스로 캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-145">You use the action property in **NotifyStateManagerChangedEventArgs** to cast **NotifyStateManagerChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="bdabd-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="bdabd-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="bdabd-147">**NotifyStateManagerChangedAction.Add** 및 **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="bdabd-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="bdabd-148">다음은 예제 **StateManagerChanged** 알림 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-148">Following is an example **StateManagerChanged** notification handler.</span></span>

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="bdabd-149">신뢰할 수 있는 사전 알림</span><span class="sxs-lookup"><span data-stu-id="bdabd-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="bdabd-150">신뢰할 수 있는 사전은 다음 이벤트에 대한 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-150">Reliable Dictionary provides notifications for the following events:</span></span>

* <span data-ttu-id="bdabd-151">Rebuild: **ReliableDictionary** 가 복구 또는 복사된 로컬 상태 또는 백업에서 해당 상태를 복구하면 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="bdabd-152">Clear: **ClearAsync** 메서드를 통해 **ReliableDictionary**의 상태를 지울 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-152">Clear: Called when the state of **ReliableDictionary** has been cleared through the **ClearAsync** method.</span></span>
* <span data-ttu-id="bdabd-153">Add: 항목이 **ReliableDictionary**에 추가될 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-153">Add: Called when an item has been added to **ReliableDictionary**.</span></span>
* <span data-ttu-id="bdabd-154">Update: **IReliableDictionary** 의 항목이 업데이트되었을 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="bdabd-155">Remove: **IReliableDictionary** 의 항목이 삭제되었을 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="bdabd-156">신뢰할 수 있는 사전 알림을 가져오려면 **IReliableDictionary**에서 **DictionaryChanaged** 이벤트 처리기에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-156">To get Reliable Dictionary notifications, you need to register with the **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="bdabd-157">이러한 이벤트 처리기를 등록하는 일반적인 위치는 **ReliableStateManager.StateManagerChanged** 추가 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-157">A common place to register with these event handlers is in the **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="bdabd-158">**IReliableDictionary**가 **IReliableStateManager**에 추가되었을 때 등록하면 알림을 놓치지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-158">Registering when **IReliableDictionary** is added to **IReliableStateManager** ensures that you won't miss any notifications.</span></span>

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="bdabd-159">**ProcessStateManagerSingleEntityNotification**은 위의 **OnStateManagerChangedHandler** 예제에서 호출하는 샘플 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-159">**ProcessStateManagerSingleEntityNotification** is the sample method that the preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="bdabd-160">위의 코드는 **DictionaryChanged**와 함께 **IReliableNotificationAsyncCallback** 인터페이스도 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-160">The preceding code sets the **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="bdabd-161">**NotifyDictionaryRebuildEventArgs**에는 비동기식으로 열거되어야 하는 **IAsyncEnumerable** 인터페이스가 포함되어 있으므로 **OnDictionaryChangedHandler** 대신 **RebuildNotificationAsyncCallback**을 통해 다시 작성 알림이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs to be enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> <span data-ttu-id="bdabd-162">위의 코드에서 다시 작성 알림 처리의 일부로, 먼저 유지 관리되던 집계된 상태가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-162">In the preceding code, as part of processing the rebuild notification, first the maintained aggregated state is cleared.</span></span> <span data-ttu-id="bdabd-163">신뢰할 수 있는 컬렉션은 새 상태로 다시 작성되므로 모든 이전 알림은 관련이 없어지기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-163">Because the reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="bdabd-164">**DictionaryChanged** 이벤트 처리기는 **NotifyDictionaryChangedEventArgs**를 사용하여 이벤트에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-164">The **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="bdabd-165">**NotifyDictionaryChangedEventArgs** 에는 5개의 하위 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="bdabd-166">**NotifyDictionaryChangedEventArgs**의 작업 속성을 사용하여 **NotifyDictionaryChangedEventArgs**를 올바른 하위 클래스로 캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-166">Use the action property in **NotifyDictionaryChangedEventArgs** to cast **NotifyDictionaryChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="bdabd-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="bdabd-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="bdabd-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="bdabd-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="bdabd-169">**NotifyDictionaryChangedAction.Add** 및 **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="bdabd-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="bdabd-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="bdabd-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="bdabd-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="bdabd-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a><span data-ttu-id="bdabd-172">추천</span><span class="sxs-lookup"><span data-stu-id="bdabd-172">Recommendations</span></span>
* <span data-ttu-id="bdabd-173">*하세요* .</span><span class="sxs-lookup"><span data-stu-id="bdabd-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="bdabd-174">*마세요* .</span><span class="sxs-lookup"><span data-stu-id="bdabd-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="bdabd-175">*하세요* .</span><span class="sxs-lookup"><span data-stu-id="bdabd-175">*Do* check the action type before you process the event.</span></span> <span data-ttu-id="bdabd-176">새 작업 형식이 나중에 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-176">New action types might be added in the future.</span></span>

<span data-ttu-id="bdabd-177">이때</span><span class="sxs-lookup"><span data-stu-id="bdabd-177">Here are some things to keep in mind:</span></span>

* <span data-ttu-id="bdabd-178">알림이 작업 실행의 일부로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-178">Notifications are fired as part of the execution of an operation.</span></span> <span data-ttu-id="bdabd-179">예를 들어 복원 작업의 마지막 단계로 복원 알림이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-179">For example, a restore notification is fired as the last step of a restore operation.</span></span> <span data-ttu-id="bdabd-180">복원은 알림 이벤트가 처리될 때까지 완료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-180">A restore will not finish until the notification event is processed.</span></span>
* <span data-ttu-id="bdabd-181">알림이 작업 적용의 일부로 실행되므로 클라이언트에는 로컬로 커밋된 작업에 대한 알림만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-181">Because notifications are fired as part of the applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="bdabd-182">작업은 로컬로만 커밋(즉, 로깅)되도록 보장되므로 나중에 실행을 취소할 수도 있고 그렇지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-182">And because operations are guaranteed only to be locally committed (in other words, logged), they might or might not be undone in the future.</span></span>
* <span data-ttu-id="bdabd-183">다시 실행 경로에서는 적용된 각 작업에 대해 단일 알림이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-183">On the redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="bdabd-184">즉, 트랜잭션 T1에 Create(X), Delete(X), Create(X)가 포함되는 경우 이 순서대로 X 생성에 대한 알림을 한 번 받고 삭제 알림을 받은 후 생성 알림을 한 번 더 받습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for the creation of X, one for the deletion, and one for the creation again, in that order.</span></span>
* <span data-ttu-id="bdabd-185">여러 작업을 포함하는 트랜잭션의 경우 작업이 사용자로부터 주 복제본에 수신된 순서대로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-185">For transactions that contain multiple operations, operations are applied in the order in which they were received on the primary replica from the user.</span></span>
* <span data-ttu-id="bdabd-186">거짓 진행률 처리의 일부로, 일부 작업이 실행 취소될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="bdabd-187">이러한 실행 취소 작업에 대해 알림이 발생하고 복제본의 상태가 안정적인 지점으로 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-187">Notifications are raised for such undo operations, rolling the state of the replica back to a stable point.</span></span> <span data-ttu-id="bdabd-188">실행 취소 알림의 중요한 차이점은 중복 키가 있는 이벤트가 집계된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="bdabd-189">예를 들어 트랜잭션 T1이 실행 취소되는 경우 Delete(X)에 대한 단일 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdabd-189">For example, if transaction T1 is being undone, you'll see a single notification to Delete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdabd-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bdabd-190">Next steps</span></span>
* [<span data-ttu-id="bdabd-191">신뢰할 수 있는 컬렉션</span><span class="sxs-lookup"><span data-stu-id="bdabd-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="bdabd-192">Reliable Services 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="bdabd-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="bdabd-193">Reliable Services 백업 및 복원(재해 복구)</span><span class="sxs-lookup"><span data-stu-id="bdabd-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="bdabd-194">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="bdabd-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

