---
title: "서비스 알림 aaaReliable | Microsoft Docs"
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
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="9c4e1-103">Reliable Services 알림</span><span class="sxs-lookup"><span data-stu-id="9c4e1-103">Reliable Services notifications</span></span>
<span data-ttu-id="9c4e1-104">알림 클라이언트 tootrack hello 변경 내용이 되 고에 관심이 있는 tooan 개체를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="9c4e1-105">*신뢰할 수 있는 상태 관리자* 및 *신뢰할 수 있는 사전*의 두 가지 개체 유형에서 알림을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="9c4e1-106">알림을 사용하는 일반적인 이유:</span><span class="sxs-lookup"><span data-stu-id="9c4e1-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="9c4e1-107">빌딩은 구체화 된 뷰 보조 인덱스와 같은 또는 필터링 된 보기 hello 복제본의 상태를 집계 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="9c4e1-108">신뢰할 수 있는 사전에 있는 모든 키의 정렬된 인덱스가 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="9c4e1-109">보내는 모니터링 데이터를 hello 지난 1 시간 동안 hello에 추가 된 사용자 수 등입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="9c4e1-110">알림은 작업 적용의 일부로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="9c4e1-111">이 때문에 알림은 가능한 한 빨리 처리되어야 하며 동기 이벤트는 광범위한 작업을 포함하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="9c4e1-112">신뢰할 수 있는 상태 관리자 알림</span><span class="sxs-lookup"><span data-stu-id="9c4e1-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="9c4e1-113">안정성 상태 관리자 이벤트를 수행 하는 hello에 대 한 알림을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="9c4e1-114">트랜잭션</span><span class="sxs-lookup"><span data-stu-id="9c4e1-114">Transaction</span></span>
  * <span data-ttu-id="9c4e1-115">커밋</span><span class="sxs-lookup"><span data-stu-id="9c4e1-115">Commit</span></span>
* <span data-ttu-id="9c4e1-116">상태 관리자</span><span class="sxs-lookup"><span data-stu-id="9c4e1-116">State manager</span></span>
  * <span data-ttu-id="9c4e1-117">다시 빌드</span><span class="sxs-lookup"><span data-stu-id="9c4e1-117">Rebuild</span></span>
  * <span data-ttu-id="9c4e1-118">신뢰할 수 있는 상태 추가</span><span class="sxs-lookup"><span data-stu-id="9c4e1-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="9c4e1-119">신뢰할 수 있는 상태 제거</span><span class="sxs-lookup"><span data-stu-id="9c4e1-119">Removal of a reliable state</span></span>

<span data-ttu-id="9c4e1-120">안정성 상태 관리자 hello 현재 처리 중 트랜잭션을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="9c4e1-121">hello만 발생 합니다. 알림 toobe 시키는 트랜잭션 상태가 변경 커밋되고 있는 트랜잭션과입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="9c4e1-122">신뢰할 수 있는 상태 관리자는 신뢰할 수 있는 사전 및 신뢰할 수 있는 큐와 같은 신뢰할 수 있는 상태 컬렉션을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="9c4e1-123">안정성 상태 관리자는이 컬렉션이 변경 될 때 알림을 발생: 신뢰할 수 있는 상태가 추가 또는 제거, 또는 hello 전체 컬렉션을 다시 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="9c4e1-124">hello 신뢰할 수 있는 상태 관리자 컬렉션 세 가지 경우에서 다시 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="9c4e1-125">복구: 복제본 시작 될 때 복구 이전 상태로 hello 디스크에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="9c4e1-126">복구의 hello 끝 사용 하 여 **NotifyStateManagerChangedEventArgs** toofire hello 일련의 복구 된 신뢰할 수 있는 상태를 포함 하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="9c4e1-127">전체 복사본: 있기 작성 toobe 복제본 hello 구성 집합에 가입 하기, 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="9c4e1-128">경우에 따라 hello 주 복제본 toobe 적용 된 toohello 유휴 보조 복제본에서 신뢰할 수 있는 상태 관리자의 상태를의 전체 복사본이 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="9c4e1-129">Hello 보조 복제본 사용에 대 한 안정성 상태 관리자 **NotifyStateManagerChangedEventArgs** toofire hello hello 주 복제본에서 획득 하는 신뢰할 수 있는 상태 집합을 포함 하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="9c4e1-130">복원의 경우 재해 복구 시나리오 hello 복제본의 상태가 복원 될 수 있습니다를 통해 백업에서 **RestoreAsync**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="9c4e1-131">Hello 주 복제본에 상태 관리자를 신뢰할 수 있는 경우에 사용 하 여 **NotifyStateManagerChangedEventArgs** toofire hello hello 백업에서 복원 하는 신뢰할 수 있는 상태 집합을 포함 하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="9c4e1-132">트랜잭션 알림을 및/또는 상태 관리자 알림 tooregister, 해야 hello로 tooregister **TransactionChanged** 또는 **StateManagerChanged** 신뢰할 수 있는 상태 관리자에서 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="9c4e1-133">공통 위치와 이러한 이벤트 처리기 tooregister 상태 저장 서비스의 hello 생성자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="9c4e1-134">hello 수명 동안 변경 내용에 의해 발생 하는 모든 알림을 얻을 수 hello 생성자를 등록 하면 **IReliableStateManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="9c4e1-135">hello **TransactionChanged** 이벤트 처리기를 사용 하 여 **NotifyTransactionChangedEventArgs** hello 이벤트에 대 한 tooprovide 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="9c4e1-136">Hello action 속성을 포함 (예를 들어 **NotifyTransactionChangedAction.Commit**) hello 변경 유형을 지정 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="9c4e1-137">또한 변경 되는 참조 toohello 트랜잭션을 제공 하는 hello 트랜잭션 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="9c4e1-138">오늘 **TransactionChanged** hello 트랜잭션이 커밋될 때 경우에 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="9c4e1-139">hello 동작은 다음 같은 너무**NotifyTransactionChangedAction.Commit**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="9c4e1-140">하지만 이후 hello, 이벤트가 다른 유형의 트랜잭션 상태 변경에 대해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="9c4e1-141">Hello 동작을 확인 하 고 하나가 있어야 하는 경우에 hello 이벤트를 처리 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="9c4e1-142">다음은 예제 **TransactionChanged** 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="9c4e1-143">hello **StateManagerChanged** 이벤트 처리기를 사용 하 여 **NotifyStateManagerChangedEventArgs** hello 이벤트에 대 한 tooprovide 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="9c4e1-144">**NotifyStateManagerChangedEventArgs**에는 두 가지 하위 클래스인 **NotifyStateManagerRebuildEventArgs**와 **NotifyStateManagerSingleEntityChangedEventArgs**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="9c4e1-145">action 속성 hello를 사용 하 여 **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello 올바른 서브 클래스:</span><span class="sxs-lookup"><span data-stu-id="9c4e1-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="9c4e1-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9c4e1-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="9c4e1-147">**NotifyStateManagerChangedAction.Add** 및 **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9c4e1-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="9c4e1-148">다음은 예제 **StateManagerChanged** 알림 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="9c4e1-149">신뢰할 수 있는 사전 알림</span><span class="sxs-lookup"><span data-stu-id="9c4e1-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="9c4e1-150">신뢰할 수 있는 사전 hello 이벤트 다음에 대 한 알림을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="9c4e1-151">Rebuild: **ReliableDictionary** 가 복구 또는 복사된 로컬 상태 또는 백업에서 해당 상태를 복구하면 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="9c4e1-152">Clear: 호출의 상태를 hello **ReliableDictionary** hello를 통해 지워진 **ClearAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="9c4e1-153">추가:에 항목이 너무 추가 될 때 호출**ReliableDictionary**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="9c4e1-154">Update: **IReliableDictionary** 의 항목이 업데이트되었을 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="9c4e1-155">Remove: **IReliableDictionary** 의 항목이 삭제되었을 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="9c4e1-156">hello로 tooregister 해야 tooget 신뢰할 수 있는 사전 알림을 **DictionaryChanged** 이벤트 처리기에 **IReliableDictionary**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="9c4e1-157">공통 위치와 이러한 이벤트 처리기 tooregister hello 중인 **ReliableStateManager.StateManagerChanged** 알림을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="9c4e1-158">등록 하는 경우 **IReliableDictionary** 너무 추가**IReliableStateManager** 알림에 얻을 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="9c4e1-159">**ProcessStateManagerSingleEntityNotification** 는 hello 샘플 메서드 앞 hello를 해당 **OnStateManagerChangedHandler** 예제 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="9c4e1-160">hello 앞의 코드 설정 hello **IReliableNotificationAsyncCallback** 함께와 상호 **DictionaryChanged**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="9c4e1-161">때문에 **NotifyDictionaryRebuildEventArgs** 포함 한 **IAsyncEnumerable** 인터페이스-비동기적으로-열거 toobe 할를 다시 작성 알림을 통해 발생 합니다.  **RebuildNotificationAsyncCallback** 대신 **OnDictionaryChangedHandler**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="9c4e1-162">Hello 처리 hello 다시 작성 하는 알림의 일환으로 코드를 앞에 오는 첫 번째 hello 집계 된 상태가 지워집니다 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="9c4e1-163">신뢰할 수 있는 컬렉션 hello 새 상태로 다시 작성 하는, 때문에 이전의 모든 알림이 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="9c4e1-164">hello **DictionaryChanged** 이벤트 처리기를 사용 하 여 **NotifyDictionaryChangedEventArgs** hello 이벤트에 대 한 tooprovide 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="9c4e1-165">**NotifyDictionaryChangedEventArgs** 에는 5개의 하위 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="9c4e1-166">action 속성 hello를 사용 하 여 **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello 올바른 서브 클래스:</span><span class="sxs-lookup"><span data-stu-id="9c4e1-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="9c4e1-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9c4e1-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="9c4e1-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9c4e1-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="9c4e1-169">**NotifyDictionaryChangedAction.Add** 및 **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9c4e1-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="9c4e1-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9c4e1-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="9c4e1-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="9c4e1-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="9c4e1-172">추천</span><span class="sxs-lookup"><span data-stu-id="9c4e1-172">Recommendations</span></span>
* <span data-ttu-id="9c4e1-173">*하세요* .</span><span class="sxs-lookup"><span data-stu-id="9c4e1-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="9c4e1-174">*마세요* .</span><span class="sxs-lookup"><span data-stu-id="9c4e1-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="9c4e1-175">*수행* hello 이벤트를 처리 하기 전에 hello 동작 종류를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="9c4e1-176">새 동작 유형에 hello 앞에 추가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="9c4e1-177">유의 사항 tookeep 몇 가지 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="9c4e1-178">알림 작업의 hello 실행의 일부로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="9c4e1-179">예를 들어 hello 복원 작업의 마지막 단계에 복원 알림이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="9c4e1-180">복원 하는 hello 알림 이벤트를 처리할 때까지 완료 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="9c4e1-181">알림 작업 적용 hello의 일부로 실행 됩니다, 때문에 클라이언트는 로컬로 커밋된 작업에 대 한 알림만 표시.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="9c4e1-182">작업은 항상 로컬로 커밋된 toobe만 않기 때문에 (즉, 로그) hello 앞에서 실행 취소 될 수 있거나 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="9c4e1-183">Hello 다시 실행 경로 적용 된 각 작업에 대해 단일 알림이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="9c4e1-184">이 트랜잭션 t 1 Create(X), Delete(X), 및 Create(X)가 포함 된 경우 하나의 알림을 받습니다 X의 hello 만들기, hello 삭제에 대 한 및 다시 hello 만들기에 대 한에 해당 순서로 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="9c4e1-185">여러 작업을 포함 하는 트랜잭션의 경우 작업이 hello hello 사용자에서 주 복제본에서 수신 된 hello 순서로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="9c4e1-186">거짓 진행률 처리의 일부로, 일부 작업이 실행 취소될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="9c4e1-187">실행 취소 작업을 롤링 hello 복제본 백 tooa 안정적인 지점 hello 상태에 대 한 알림이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="9c4e1-188">실행 취소 알림의 중요한 차이점은 중복 키가 있는 이벤트가 집계된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="9c4e1-189">예를 들어 트랜잭션 t 1을 실행 취소 하는 경우 단일 알림 tooDelete(X) 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c4e1-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c4e1-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c4e1-190">Next steps</span></span>
* [<span data-ttu-id="9c4e1-191">신뢰할 수 있는 컬렉션</span><span class="sxs-lookup"><span data-stu-id="9c4e1-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="9c4e1-192">Reliable Services 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="9c4e1-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="9c4e1-193">Reliable Services 백업 및 복원(재해 복구)</span><span class="sxs-lookup"><span data-stu-id="9c4e1-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="9c4e1-194">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="9c4e1-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

