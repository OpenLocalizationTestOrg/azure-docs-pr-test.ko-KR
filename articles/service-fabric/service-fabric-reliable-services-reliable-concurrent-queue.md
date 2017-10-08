---
title: "Azure 서비스 패브릭에서 aaaReliableConcurrentQueue"
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
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>Azure 서비스 패브릭에서 tooReliableConcurrentQueue 소개
신뢰할 수 있는 동시 큐는 비동기, 트랜잭션 및 복제된 큐로서 큐에 넣기 및 큐에서 제거 작업에 대한 높은 동시성을 제공합니다. 디자인 된 toodeliver 높은 처리량 및 짧은 대기 시간 완화 hello 엄격한 FIFO 순서에서 제공 하 여 [신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx) 대신 최상의 순서를 제공 합니다.

## <a name="apis"></a>API

|동시 큐                |신뢰할 수 있는 동시 큐                                         |
|--------------------------------|------------------------------------------------------------------|
| void Enqueue(T item)           | Task EnqueueAsync(ITransaction tx, T item)                       |
| bool TryDequeue(out T result)  | Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)  |
| int Count()                    | long Count()                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>[신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx)와 비교

신뢰할 수 있는 동시 큐 대신 너무 제공[신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx)합니다. FIFO 보장은 동시성을 상쇄해야 하기 때문에 엄격한 FIFO 순서가 필요하지 않은 경우에 사용해야 합니다.  [신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx) 잠금을 tooenforce FIFO 순서 지정 tooenqueue 허용 되는 최대 하나의 트랜잭션 및 가장 많이 toodequeue 한 번에 허용 된 트랜잭션을 최대 하나만 사용 합니다. 비교에서 신뢰할 수 있는 동시 큐 모든 숫자 동시 트랜잭션이 toointerleave 해당 큐에 넣을 수 있습니다 및 큐에서 제거 작업 hello 순서 제약 조건을 완화 합니다. 하지만 최상의 순서는 보장 신뢰할 수 있는 동시 큐에 있는 두 값의 상대적 순서 hello 수 제공 됩니다.

여러 동시 트랜잭션이 큐에 넣기 및/또는 큐에서 제거를 수행할 때 신뢰할 수 있는 동시 큐는 [신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx)보다 처리량이 높고 대기 시간이 낮습니다.

샘플 사용 사례는 hello hello ReliableConcurrentQueue [메시지 큐](https://en.wikipedia.org/wiki/Message_queue) 시나리오입니다. 이 시나리오에서는 하나 이상의 메시지 생산자를 만들고 항목 toohello 큐에 추가 하 고 hello 큐에서 메시지를 끌어올 하 고 처리 하는 메시지 소비자 하나 이상의 합니다. 여러 생산자와 소비자 수 독립적으로 작업 순서 tooprocess hello 큐에서 동시 트랜잭션을 사용 합니다.

## <a name="usage-guidelines"></a>사용 지침
* hello 큐는 hello 큐의 hello 항목 낮은 보존 기간이 필요 합니다. 즉, hello 항목은 오랜 시간 동안 hello 큐에 남아 있지입니다.
* hello 큐는 엄격한 FIFO 순서를 보장 하지 않습니다.
* hello 큐 자체 쓰기 읽을 수 없습니다. Hello 내 표시 tooa dequeuer 않을 트랜잭션 내에서 큐에 대기 된 항목의 경우 동일한 트랜잭션.
* 큐에서 제거는 서로 분리되지 않습니다. 항목 *A* 트랜잭션으로 큐에서 제거 *txnA*경우라도, *txnA* 항목, 커밋되지 않은 *A* 됩니다 표시 tooa 동시 트랜잭션 *txnB*합니다.  경우 *txnA* 중단 되 면 *A* 너무 표시 될*txnB* 즉시 합니다.
* *TryPeekAsync* 동작을 사용 하 여 구현할 수 있습니다는 *TryDequeueAsync* 다음 hello 트랜잭션을 중단 하 고 있습니다. 이러한 예는 hello 프로그래밍 패턴 섹션에서에서 찾을 수 있습니다.
* 개수는 비트랜잭션입니다. 사용된 tooget hello hello 큐에 있는 요소 수에 대해 알 수 있지만 지정-에-시간 나타내며에 의존할 수 없습니다.
* Hello에 대 한 처리 비용이 많이 드는 큐에서 제거 된 항목을 수행 하지 않도록 hello 트랜잭션이 활성 중일 tooavoid 장기 실행 트랜잭션을 hello 시스템에 성능에 주는 영향이 있을 수 있습니다.

## <a name="code-snippets"></a>코드 조각
몇 가지 코드 조각 및 예상된 출력에 대해 살펴보겠습니다. 이 섹션에서 예외 처리는 무시됩니다.

### <a name="enqueueasync"></a>EnqueueAsync
다음은 예상된 출력 뒤에 EnqueueAsync를 사용하기 위한 몇 가지 코드 조각입니다.

- *사례 1: 단일 큐에 넣기 작업*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

Hello 큐를 수정 하는 트랜잭션은 동시 트랜잭션이 없는 있었습니다 하 고 성공적으로 완료 하는 hello 작업을 가정 합니다. hello 사용자 hello 주문 다음 중 하나에 hello 큐 toocontain hello 항목 될 수 있습니다.

> 10, 20

> 20, 10


- *사례 2: 병렬 큐에 넣기 작업*

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

hello 작업에서 병렬로 실행 하 고 다른 트랜잭션은 동시 트랜잭션이 없는 hello 큐 수정 했음을 hello 작업이 성공적으로 완료 하는 것으로 가정 합니다. Hello 순서 hello 큐의 항목에 대 한 없습니다 유추를 만들 수 있습니다. 이 코드 조각에 대 한 hello 항목 4 hello에 나타날 수 있습니다! 가능한 순서로 정렬 되어 있습니다.  hello 큐 tookeep hello 항목 순서로 hello 원래 (큐), 되지만 강제 tooreorder 않을 수 있습니다 기한 tooconcurrent 작업 또는 오류가 발생 합니다.


### <a name="dequeueasync"></a>DequeueAsync
다음은 TryDequeueAsync hello 예상 출력 뒤에 사용 하기 위한 몇 가지 코드 조각입니다. 해당 hello 큐 hello hello 큐에 있는 항목을 다음으로 이미 채워져 가정 합니다.
> 10, 20, 30, 40, 50, 60

- *사례 1: 단일 큐에서 제거 작업*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

Hello 큐를 수정 하는 트랜잭션은 동시 트랜잭션이 없는 있었습니다 하 고 성공적으로 완료 하는 hello 작업을 가정 합니다. 없는 유추 hello 큐의 hello 항목 hello 순서에 대 한 만들어질 수 있으므로 모든 세 항목이 hello 수 있습니다 수 큐에서 제거를 순서에 관계 없이 합니다. hello 큐 tookeep hello 항목 순서로 hello 원래 (큐), 되지만 강제 tooreorder 않을 수 있습니다 기한 tooconcurrent 작업 또는 오류가 발생 합니다.  

- *사례 2: 병렬 큐에서 제거 작업*

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

hello 작업에서 병렬로 실행 하 고 다른 트랜잭션은 동시 트랜잭션이 없는 hello 큐 수정 했음을 hello 작업이 성공적으로 완료 하는 것으로 가정 합니다. 없는 유추 hello 큐의 hello 항목 hello 순서에 대 한 만들어질 수 있으므로 hello 목록 *dequeue1* 및 *dequeue2* 각각 순서에 관계 없이 두 개의 항목이 포함 됩니다.

동일한 항목은 hello *하지* 두 목록에에서 표시 합니다. 따라서 dequeue1에 *10*, *30*이 있으면 dequeue2에는 *20*, *40*이 포함됩니다.

- *사례 3: 트랜잭션이 중단된 큐에서 제거 순서*

진행 중인 인 트랜잭션을 중단 하 고 hello 항목 hello 큐의 hello 헤드에 대해 설정 큐에서 제거 합니다. hello 항목 hello 큐의 앞 부분 hello에 넣는 다시 hello 순서 보장 되지 않습니다. 에 대해 알아보겠습니다 코드 다음 hello:

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
순서에 따라 hello에 hello 항목 된 큐에서 제거를 가정 합니다.
> 10, 20

Hello 트랜잭션을 중단 하는 것 때 hello 항목 추가 되 hello 큐의 앞 부분 백 toohello hello 주문 다음 중 하나:
> 10, 20

> 20, 10

hello에 마찬가지입니다 hello 트랜잭션의 푼 성공적으로 모든 경우 *커밋됨*합니다.

## <a name="programming-patterns"></a>프로그래밍 패턴
이 섹션에서는 ReliableConcurrentQueue를 사용하는 데 도움이 될 수 있는 몇 가지 프로그래밍 패턴을 살펴보겠습니다.

### <a name="batch-dequeues"></a>큐에서 제거 일괄 처리
A 소비자 작업 toobatch hello에 대 한 프로그래밍 패턴은 권장의 하나를 수행 하는 대신 큐에서 한 번에 큐에서 제거 합니다. hello 사용자는 모든 일괄 처리 또는 hello 일괄 처리 크기 간에 toothrottle 지연 선택할 수 있습니다. hello 다음 코드 조각은이 프로그래밍 모델을 보여줍니다.  이 예제에서는 hello 처리 했는지 hello 트랜잭션이 커밋된 후 되도록 오류 처리 하는 동안 toooccur 인 경우 hello 처리 되지 않은 항목 손실 처리 된 필요 없이 note 합니다.  하지만 Hello 처리를 수행할 수 있습니다 또는 hello 트랜잭션 범위 내에서이 성능에 부정적인 영향을 미칠 수 있습니다 및 이미 hello 항목 처리가 필요 처리 합니다.

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
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a>최상의 알림 기반 처리
또 다른 흥미로운 프로그래밍 패턴 hello 개수 API를 사용합니다. 여기에서는 hello 큐에 대 한 최상의 알림 기반 처리를 구현할 수 있습니다. hello 큐 개수 인 큐에서 사용 되는 toothrottle 또는 큐에서 제거 작업 수 있습니다.  참고 hello 이전 예제와 같이 hello 처리 hello 트랜잭션 밖에 서 발생 하므로 처리 되지 않은 항목이 손실 될 수 있다는 처리 하는 동안 오류가 발생 하는 경우.

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

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
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a>최상의 드레이닝
Hello 데이터 구조의 toohello 동시 특성 인해 hello 큐의 드레이닝을 보장할 수 없습니다.  즉, hello 큐에 없는 사용자는 작업은 진행 중인, 경우에 특정 호출 tooTryDequeueAsync 반환할 수 없습니다. 큐에 대기 된 이전의 항목 수 및 커밋되지 않습니다.  하지만 hello 큐에 대기 된 항목은 너무 보장*결국* 는-대역외 통신 메커니즘 없이 독립 소비자를 알 수 없으므로 해당 hello 큐에 경우에도 안정 상태에 도달 했습니다 표시 toodequeue 될 모든 생산자를 중지 하 고 새 큐에 삽입 작업이 허용 되지 않습니다. 따라서 hello 드레이닝 작업이 최상의 아래 구현입니다.

hello 사용자는 모든 후속 생산자와 소비자 작업을 중지 하 고 모든 진행 중인 트랜잭션은 toocommit 또는 중단 toodrain hello 큐를 시도 하기 전에 대기 해야 합니다.  Hello 사용자가 예상 하는 hello hello 큐의 항목 수를 알고, 모든 항목이 있는 큐 제거 알리는 알림을 설정할 수 있습니다.

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
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a>보기
ReliableConcurrentQueue hello를 제공 하지 않습니다 *TryPeekAsync* api입니다. 사용자가 액세스할 수 hello 피크 (peek) 의미 체계를 사용 하 여 한 *TryDequeueAsync* 다음 hello 트랜잭션을 중단 하 고 있습니다. 이 예제에서는 큐에서 hello 항목의 값 보다 큰 경우에 처리 *10*합니다.

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
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

## <a name="must-read"></a>필수 참고 목록
* [Reliable Services 빠른 시작](service-fabric-reliable-services-quick-start.md)
* [신뢰할 수 있는 컬렉션 작업](service-fabric-work-with-reliable-collections.md)
* [Reliable Services 알림](service-fabric-reliable-services-notifications.md)
* [Reliable Services 백업 및 복원(재해 복구)](service-fabric-reliable-services-backup-restore.md)
* [신뢰할 수 있는 상태 관리자 구성](service-fabric-reliable-services-configuration.md)
* [Service Fabric Web API 서비스 시작](service-fabric-reliable-services-communication-webapi.md)
* [Hello 신뢰할 수 있는 서비스 프로그래밍 모델의 고급 사용](service-fabric-reliable-services-advanced-usage.md)
* [신뢰할 수 있는 컬렉션에 대한 개발자 참조](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
