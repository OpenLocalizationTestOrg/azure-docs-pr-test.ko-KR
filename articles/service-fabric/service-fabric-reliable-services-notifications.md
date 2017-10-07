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
# <a name="reliable-services-notifications"></a>Reliable Services 알림
알림 클라이언트 tootrack hello 변경 내용이 되 고에 관심이 있는 tooan 개체를 허용 합니다. *신뢰할 수 있는 상태 관리자* 및 *신뢰할 수 있는 사전*의 두 가지 개체 유형에서 알림을 지원합니다.

알림을 사용하는 일반적인 이유:

* 빌딩은 구체화 된 뷰 보조 인덱스와 같은 또는 필터링 된 보기 hello 복제본의 상태를 집계 합니다. 신뢰할 수 있는 사전에 있는 모든 키의 정렬된 인덱스가 그 예입니다.
* 보내는 모니터링 데이터를 hello 지난 1 시간 동안 hello에 추가 된 사용자 수 등입니다.

알림은 작업 적용의 일부로 실행됩니다. 이 때문에 알림은 가능한 한 빨리 처리되어야 하며 동기 이벤트는 광범위한 작업을 포함하지 않아야 합니다.

## <a name="reliable-state-manager-notifications"></a>신뢰할 수 있는 상태 관리자 알림
안정성 상태 관리자 이벤트를 수행 하는 hello에 대 한 알림을 제공 합니다.

* 트랜잭션
  * 커밋
* 상태 관리자
  * 다시 빌드
  * 신뢰할 수 있는 상태 추가
  * 신뢰할 수 있는 상태 제거

안정성 상태 관리자 hello 현재 처리 중 트랜잭션을 추적합니다. hello만 발생 합니다. 알림 toobe 시키는 트랜잭션 상태가 변경 커밋되고 있는 트랜잭션과입니다.

신뢰할 수 있는 상태 관리자는 신뢰할 수 있는 사전 및 신뢰할 수 있는 큐와 같은 신뢰할 수 있는 상태 컬렉션을 유지 관리합니다. 안정성 상태 관리자는이 컬렉션이 변경 될 때 알림을 발생: 신뢰할 수 있는 상태가 추가 또는 제거, 또는 hello 전체 컬렉션을 다시 작성 됩니다.
hello 신뢰할 수 있는 상태 관리자 컬렉션 세 가지 경우에서 다시 작성 됩니다.

* 복구: 복제본 시작 될 때 복구 이전 상태로 hello 디스크에서 합니다. 복구의 hello 끝 사용 하 여 **NotifyStateManagerChangedEventArgs** toofire hello 일련의 복구 된 신뢰할 수 있는 상태를 포함 하는 이벤트입니다.
* 전체 복사본: 있기 작성 toobe 복제본 hello 구성 집합에 가입 하기, 전에 합니다. 경우에 따라 hello 주 복제본 toobe 적용 된 toohello 유휴 보조 복제본에서 신뢰할 수 있는 상태 관리자의 상태를의 전체 복사본이 있어야합니다. Hello 보조 복제본 사용에 대 한 안정성 상태 관리자 **NotifyStateManagerChangedEventArgs** toofire hello hello 주 복제본에서 획득 하는 신뢰할 수 있는 상태 집합을 포함 하는 이벤트입니다.
* 복원의 경우 재해 복구 시나리오 hello 복제본의 상태가 복원 될 수 있습니다를 통해 백업에서 **RestoreAsync**합니다. Hello 주 복제본에 상태 관리자를 신뢰할 수 있는 경우에 사용 하 여 **NotifyStateManagerChangedEventArgs** toofire hello hello 백업에서 복원 하는 신뢰할 수 있는 상태 집합을 포함 하는 이벤트입니다.

트랜잭션 알림을 및/또는 상태 관리자 알림 tooregister, 해야 hello로 tooregister **TransactionChanged** 또는 **StateManagerChanged** 신뢰할 수 있는 상태 관리자에서 이벤트입니다. 공통 위치와 이러한 이벤트 처리기 tooregister 상태 저장 서비스의 hello 생성자가 있습니다. hello 수명 동안 변경 내용에 의해 발생 하는 모든 알림을 얻을 수 hello 생성자를 등록 하면 **IReliableStateManager**합니다.

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

hello **TransactionChanged** 이벤트 처리기를 사용 하 여 **NotifyTransactionChangedEventArgs** hello 이벤트에 대 한 tooprovide 세부 정보입니다. Hello action 속성을 포함 (예를 들어 **NotifyTransactionChangedAction.Commit**) hello 변경 유형을 지정 하 합니다. 또한 변경 되는 참조 toohello 트랜잭션을 제공 하는 hello 트랜잭션 속성을 포함 합니다.

> [!NOTE]
> 오늘 **TransactionChanged** hello 트랜잭션이 커밋될 때 경우에 이벤트가 발생 합니다. hello 동작은 다음 같은 너무**NotifyTransactionChangedAction.Commit**합니다. 하지만 이후 hello, 이벤트가 다른 유형의 트랜잭션 상태 변경에 대해 발생할 수 있습니다. Hello 동작을 확인 하 고 하나가 있어야 하는 경우에 hello 이벤트를 처리 하는 것이 좋습니다.
> 
> 

다음은 예제 **TransactionChanged** 이벤트 처리기입니다.

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

hello **StateManagerChanged** 이벤트 처리기를 사용 하 여 **NotifyStateManagerChangedEventArgs** hello 이벤트에 대 한 tooprovide 세부 정보입니다.
**NotifyStateManagerChangedEventArgs**에는 두 가지 하위 클래스인 **NotifyStateManagerRebuildEventArgs**와 **NotifyStateManagerSingleEntityChangedEventArgs**가 있습니다.
action 속성 hello를 사용 하 여 **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello 올바른 서브 클래스:

* **NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**
* **NotifyStateManagerChangedAction.Add** 및 **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**

다음은 예제 **StateManagerChanged** 알림 처리기입니다.

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

## <a name="reliable-dictionary-notifications"></a>신뢰할 수 있는 사전 알림
신뢰할 수 있는 사전 hello 이벤트 다음에 대 한 알림을 제공 합니다.

* Rebuild: **ReliableDictionary** 가 복구 또는 복사된 로컬 상태 또는 백업에서 해당 상태를 복구하면 호출됩니다.
* Clear: 호출의 상태를 hello **ReliableDictionary** hello를 통해 지워진 **ClearAsync** 메서드.
* 추가:에 항목이 너무 추가 될 때 호출**ReliableDictionary**합니다.
* Update: **IReliableDictionary** 의 항목이 업데이트되었을 때 호출됩니다.
* Remove: **IReliableDictionary** 의 항목이 삭제되었을 때 호출됩니다.

hello로 tooregister 해야 tooget 신뢰할 수 있는 사전 알림을 **DictionaryChanged** 이벤트 처리기에 **IReliableDictionary**합니다. 공통 위치와 이러한 이벤트 처리기 tooregister hello 중인 **ReliableStateManager.StateManagerChanged** 알림을 추가 합니다.
등록 하는 경우 **IReliableDictionary** 너무 추가**IReliableStateManager** 알림에 얻을 수 있는지 확인 합니다.

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
> **ProcessStateManagerSingleEntityNotification** 는 hello 샘플 메서드 앞 hello를 해당 **OnStateManagerChangedHandler** 예제 호출 합니다.
> 
> 

hello 앞의 코드 설정 hello **IReliableNotificationAsyncCallback** 함께와 상호 **DictionaryChanged**합니다. 때문에 **NotifyDictionaryRebuildEventArgs** 포함 한 **IAsyncEnumerable** 인터페이스-비동기적으로-열거 toobe 할를 다시 작성 알림을 통해 발생 합니다.  **RebuildNotificationAsyncCallback** 대신 **OnDictionaryChangedHandler**합니다.

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
> Hello 처리 hello 다시 작성 하는 알림의 일환으로 코드를 앞에 오는 첫 번째 hello 집계 된 상태가 지워집니다 유지 관리 합니다. 신뢰할 수 있는 컬렉션 hello 새 상태로 다시 작성 하는, 때문에 이전의 모든 알림이 적용 되지 않습니다.
> 
> 

hello **DictionaryChanged** 이벤트 처리기를 사용 하 여 **NotifyDictionaryChangedEventArgs** hello 이벤트에 대 한 tooprovide 세부 정보입니다.
**NotifyDictionaryChangedEventArgs** 에는 5개의 하위 클래스가 있습니다. action 속성 hello를 사용 하 여 **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello 올바른 서브 클래스:

* **NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**
* **NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**
* **NotifyDictionaryChangedAction.Add** 및 **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**
* **NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**
* **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**

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

## <a name="recommendations"></a>추천
* *하세요* .
* *마세요* .
* *수행* hello 이벤트를 처리 하기 전에 hello 동작 종류를 확인 합니다. 새 동작 유형에 hello 앞에 추가 될 수 있습니다.

유의 사항 tookeep 몇 가지 다음과 같습니다.

* 알림 작업의 hello 실행의 일부로 발생 합니다. 예를 들어 hello 복원 작업의 마지막 단계에 복원 알림이 발생 합니다. 복원 하는 hello 알림 이벤트를 처리할 때까지 완료 되지 않습니다.
* 알림 작업 적용 hello의 일부로 실행 됩니다, 때문에 클라이언트는 로컬로 커밋된 작업에 대 한 알림만 표시. 작업은 항상 로컬로 커밋된 toobe만 않기 때문에 (즉, 로그) hello 앞에서 실행 취소 될 수 있거나 수도 있습니다.
* Hello 다시 실행 경로 적용 된 각 작업에 대해 단일 알림이 발생 합니다. 이 트랜잭션 t 1 Create(X), Delete(X), 및 Create(X)가 포함 된 경우 하나의 알림을 받습니다 X의 hello 만들기, hello 삭제에 대 한 및 다시 hello 만들기에 대 한에 해당 순서로 것을 의미 합니다.
* 여러 작업을 포함 하는 트랜잭션의 경우 작업이 hello hello 사용자에서 주 복제본에서 수신 된 hello 순서로 적용 됩니다.
* 거짓 진행률 처리의 일부로, 일부 작업이 실행 취소될 수 있습니다. 실행 취소 작업을 롤링 hello 복제본 백 tooa 안정적인 지점 hello 상태에 대 한 알림이 발생 합니다. 실행 취소 알림의 중요한 차이점은 중복 키가 있는 이벤트가 집계된다는 것입니다. 예를 들어 트랜잭션 t 1을 실행 취소 하는 경우 단일 알림 tooDelete(X) 표시 됩니다.

## <a name="next-steps"></a>다음 단계
* [신뢰할 수 있는 컬렉션](service-fabric-work-with-reliable-collections.md)
* [Reliable Services 빠른 시작](service-fabric-reliable-services-quick-start.md)
* [Reliable Services 백업 및 복원(재해 복구)](service-fabric-reliable-services-backup-restore.md)
* [신뢰할 수 있는 컬렉션에 대한 개발자 참조](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

