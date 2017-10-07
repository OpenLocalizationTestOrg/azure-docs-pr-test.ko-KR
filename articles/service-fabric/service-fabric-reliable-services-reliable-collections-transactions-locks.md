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
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a>Azure Service Fabric 신뢰할 수 있는 컬렉션의 트랜잭션 및 잠금 모드

## <a name="transaction"></a>트랜잭션
트랜잭션은 작업의 단일 논리적 단위로 수행되는 작업 시퀀스입니다.
트랜잭션이 다음 트랜잭션의 ACID 속성이 hello를 시 해야 합니다. (참조: https://technet.microsoft.com/en-us/library/ms190612)
* **원자성**: 트랜잭션은 작업의 원자 단위여야 합니다. 즉, 모든 데이터 수정 작업이 수행되거나, 또는 하나도 수행되지 않아야 합니다.
* **일관성**: 완료되면 트랜잭션은 모든 데이터를 일관된 상태로 유지해야 합니다. 모든 내부 데이터 구조는 hello hello 트랜잭션이 끝나기 전에 정확 해야 합니다.
* **격리**: 수정한 동시 트랜잭션이 다른 동시 트랜잭션에 의해 hello 수정 되지 않도록에서 격리 되어야 합니다. ITransaction 내에서 작업에 사용 되는 hello 격리 수준은 hello IReliableState 수행 되는 hello 작업에 의해 결정 됩니다.
* **내구성**: 트랜잭션이 완료 되 면 그 효과 영구적으로 준비에서 hello s입니다. hello 수정은 시스템 오류의 hello 이벤트에도 지속 합니다.

### <a name="isolation-levels"></a>격리 수준
Hello 정도 정의 하는 격리 수준을 toowhich hello 트랜잭션 다른 트랜잭션에 의해 수정 되지 않도록에서 격리 되어야 합니다.
신뢰할 수 있는 컬렉션에서 지원되는 두 격리 수준이 있습니다.

* **반복 읽기**: 문이 수정 되었지만 아직 커밋되지 않은 다른 트랜잭션에서 데이터를 읽을 수 없도록 하 고 다른 트랜잭션이 현재 hello까지 hello 현재 트랜잭션에서 읽은 데이터를 수정할 수 있는지를 지정 합니다. 트랜잭션을 완료합니다. 자세한 내용은 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)를 참조하세요.
* **스냅숏**: 트랜잭션의 모든 문에서 읽는 데이터 hello와 버전의 일관성이 hello hello 트랜잭션 시작 시 hello 데이터를 지정 합니다.
  hello 트랜잭션 hello hello 트랜잭션이 시작 되기 전에 커밋된 데이터 수정 내용만 인식할 수 있습니다.
  Hello hello 현재 트랜잭션의 시작 이후 다른 트랜잭션에서 발생 수정한 데이터 표시 toostatements hello 현재 트랜잭션에서 실행 되지 않습니다.
  hello hello hello 트랜잭션 시작 당시 hello 문은 hello 커밋된 데이터의 스냅숏을 가져오는 처럼 같습니다.
  스냅숏은 신뢰할 수 있는 컬렉션 간에 일관됩니다.
  자세한 내용은 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)를 참조하세요.

신뢰할 수 있는 컬렉션 hello 트랜잭션의 생성 시 hello 작업과 hello 복제본의 hello 역할에 따라 지정 된 읽기 작업이 격리 수준 toouse hello를 자동으로 선택합니다.
다음은 신뢰할 수 있는 사전 및 큐 작업에 대 한 격리 수준 기본값을 보여 주는 hello 테이블입니다.

| 작업 \ 역할 | 보조 | 주 |
| --- |:--- |:--- |
| 단일 엔터티 읽기 |반복 가능한 읽기 |스냅숏 |
| 열거형, 개수 |스냅숏 |스냅숏 |

> [!NOTE]
> 단일 엔터티 작업에 대한 일반적인 예제는 `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`입니다.
> 

신뢰할 수 있는 사전 hello와 hello 신뢰할 수 있는 큐 읽기 Your 작성을 지원합니다.
트랜잭션 내에서 표시 tooa 다음 읽을 toohello 속하는 쓰기 즉, 동일한 트랜잭션.

## <a name="locks"></a>잠금
신뢰할 수 있는 컬렉션에서 모든 트랜잭션을 구현 엄격한 2 단계 잠금: 트랜잭션 중단 또는 커밋 hello 트랜잭션이 종료 될 때까지 확보 한 hello 잠금 해제 하지 않습니다.

신뢰할 수 있는 사전은 모든 단일 엔터티 작업에 대해 행 수준 잠금을 사용합니다.
신뢰할 수 있는 큐와 엄격한 트랜잭션 FIFO 속성의 동시성은 서로 균형을 유지합니다.
신뢰할 수 있는 큐는 작업 수준 잠금을 사용하여 한 번에 한 트랜잭션에는 `TryPeekAsync` 및/또는 `TryDequeueAsync`를 허용하고, 다른 트랜잭션에는 `EnqueueAsync`를 허용합니다.
참고 해당 toopreserve FIFO, 경우에 `TryPeekAsync` 또는 `TryDequeueAsync` hello 신뢰할 수 있는 큐가 비어, 또한 잠급니다 적이 관찰 `EnqueueAsync`합니다.

쓰기 작업은 항상 배타적 잠금을 수행합니다.
읽기 작업 hello 잠금에 여러 요인에 따라 다릅니다.
스냅숏 격리를 사용하여 수행된 모든 읽기 작업은 잠금이 없습니다.
모든 반복 가능한 읽기 작업은 기본적으로 공유 잠금을 수행합니다.
그러나 반복 가능한 읽기를 지 원하는 모든 읽기 작업, hello 사용자 hello 공유 잠금 대신 업데이트 잠금에 대 한 요청할 수 있습니다.
업데이트 잠금은 비대칭 잠금 tooprevent 일반적인 형태의 교착 상태 여러 트랜잭션을 나중에 업데이트에 대 한 리소스를 잠글 때 발생 하는 데 사용 됩니다.

다음 표에 hello에 hello 잠금 호환성 표를 찾을 수 있습니다.

| 요청 \ 부여 | 없음 | 공유됨 | 업데이트 | 단독 |
| --- |:--- |:--- |:--- |:--- |
| 공유됨 |충돌 없음 |충돌 없음 |충돌 |충돌 |
| 업데이트 |충돌 없음 |충돌 없음 |충돌 |충돌 |
| 단독 |충돌 없음 |충돌 |충돌 |충돌 |

제한 시간 인수가 hello 신뢰할 수 있는 컬렉션 Api에서에서 교착 상태 감지에 사용 됩니다.
예를 들어 두 개의 트랜잭션 (t 1과 T2) tooread 시도 하 고 K1를 업데이트 합니다.
공유할 수는 toodeadlock, 결국 모두 때문에 잠금 공유 hello 필요 합니다.
이 경우 하나 또는 둘 다 hello 작업 시간이 초과 됩니다.

이 교착 상태 시나리오는 업데이트 잠금이 교착 상태를 방지하는 방법을 보여주는 좋은 예입니다.

## <a name="next-steps"></a>다음 단계
* [신뢰할 수 있는 컬렉션 작업](service-fabric-work-with-reliable-collections.md)
* [Reliable Services 알림](service-fabric-reliable-services-notifications.md)
* [Reliable Services 백업 및 복원(재해 복구)](service-fabric-reliable-services-backup-restore.md)
* [신뢰할 수 있는 상태 관리자 구성](service-fabric-reliable-services-configuration.md)
* [신뢰할 수 있는 컬렉션에 대한 개발자 참조](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

