---
title: "Azure 서비스 패브릭 상태 저장 서비스에 대 한 컬렉션 aaaIntroduction tooReliable | Microsoft Docs"
description: "서비스 패브릭 상태 저장 서비스를 사용 하면 신뢰할 수 있는 컬렉션 toowrite 항상 사용 가능한 가능 하 고 대기 시간이 짧은 클라우드 응용 프로그램을 제공 합니다."
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
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>Azure 서비스 패브릭 상태 저장 서비스의 컬렉션 소개 tooReliable
신뢰할 수 있는 컬렉션 사용 하면 항상 사용 가능한 가능 하 고 대기 시간이 짧은 클라우드 응용 프로그램 toowrite 단일 컴퓨터 응용 프로그램을 작성 하는 것에 처럼 있습니다. hello의 클래스 hello **Microsoft.ServiceFabric.Data.Collections** 네임 스페이스는 컬렉션에 자동으로 항상 사용 가능 상태 집합을 제공 합니다. 개발자가 tooprogram만 toohello 신뢰할 수 있는 컬렉션 Api 필요를 복제 하는 hello 및 로컬 상태를 관리 하는 신뢰할 수 있는 컬렉션 됩니다.

신뢰할 수 있는 컬렉션 및 다른 고가용성 기술 (예: Redis, Azure 테이블 서비스 및 Azure 큐 서비스) 간의 hello 주요 차이점 hello 상태가 유지 되도록 로컬로 hello 서비스 인스턴스의 항상 사용할 수 있게 되는 동안입니다. 이는 다음을 의미합니다.

* 모든 읽기가 로컬이므로 대기 시간이 짧고 처리량이 많습니다.
* 모든 쓰기 hello 최소 네트워크 Io 수를 낮은 대기 시간에 발생 하 고 처리량이 높은 씁니다.

![컬렉션 진화 이미지](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

신뢰할 수 있는 컬렉션의 hello 자연 스런 hello로 생각할 수 있습니다 **System.Collections** 클래스:에 대 한 복잡성을 늘리지 않고도 hello 클라우드 및 다중 컴퓨터 응용 프로그램을 위해 디자인 된 컬렉션의 새 집합 hello 개발자입니다. 따라서 신뢰할 수 있는 컬렉션은 다음과 같습니다.

* 복제됨: 고가용성을 위해 상태 변경 내용이 복제됩니다.
* Persisted: 데이터는 대규모 작동 중단 (예를 들어 데이터 센터 정전)에 대 한 내구성에 대 한 지속형된 toodisk 됩니다.
* 비동기: Api는 비동기 tooensure IO를 초래 하는 경우 스레드가 차단 되지 않으므로 합니다.
* 트랜잭션: Api 활용 트랜잭션의 hello 추상화 서비스 내에서 신뢰할 수 있는 여러 컬렉션을 쉽게 관리할 수 있도록 합니다.

신뢰할 수 있는 컬렉션에서 보다 쉽게 응용 프로그램 상태에 대 한 추론 hello 상자 toomake 강력한 일관성은 보장은 제공 합니다.
강력한 일관성 트랜잭션 커밋 hello 주를 포함 하 여 복제본의 과반수 쿼럼에 hello 전체 트랜잭션을 기록한 후에 완료 되도록 하 여 이루어집니다.
tooachieve 약한 일관성 응용 프로그램 백 toohello 클라이언트/요청자를 승인 하 수 hello 비동기 커밋 반환 되기 전에 합니다.

hello 신뢰할 수 있는 컬렉션 Api는 동시 컬렉션 Api의 진화 (hello에 **System.Collections.Concurrent** 네임 스페이스):

* 비동기: 작업 이후 동시 컬렉션와 달리 hello 작업은 복제 되 고 지속 반환 합니다.
* Out 매개 변수 더: 사용 하 여 `ConditionalValue<T>` tooreturn bool 점과 out 매개 변수 값 대신 합니다. `ConditionalValue<T>`비슷합니다 `Nullable<T>` 하지만 T toobe 구조체는 필요 하지 않습니다.
* 트랜잭션: 트랜잭션에서 여러 신뢰할 수 있는 컬렉션에 대 한 트랜잭션 개체 tooenable hello 사용자 toogroup 동작을 사용 하 합니다.

오늘날 **Microsoft.ServiceFabric.Data.Collections** 은 다음과 같은 3가지 컬렉션을 포함합니다.

* [신뢰할 수 있는 사전](https://msdn.microsoft.com/library/azure/dn971511.aspx): 키/값 쌍의 복제, 트랜잭션 및 비동기 컬렉션을 나타냅니다. 비슷한 너무**ConcurrentDictionary**, 둘 다 hello 키 및 모든 종류의 hello 값일 수 있습니다.
* [신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx): 복제, 트랜잭션 및 비동기의 엄격한 FIFO(선입 선출) 큐를 나타냅니다. 비슷한 너무**ConcurrentQueue**, hello 값은 모든 유형일 수 있습니다.
* [신뢰할 수 있는 동시 큐](service-fabric-reliable-services-reliable-concurrent-queue.md): 높은 처리량을 위해 최고의 순서로 대기되는 복제, 트랜잭션 및 비동기 큐. 비슷한 toohello **ConcurrentQueue**, hello 값은 모든 유형일 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [신뢰할 수 있는 컬렉션 지침 및 권장 사항](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [신뢰할 수 있는 컬렉션 작업](service-fabric-work-with-reliable-collections.md)
* [트랜잭션 및 잠금](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [신뢰할 수 있는 상태 관리자 및 컬렉션 내부](service-fabric-reliable-services-reliable-collections-internals.md)
* 데이터 관리
  * [백업 및 복원](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [신뢰할 수 있는 컬렉션 serialization](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [Serialization 및 업그레이드](service-fabric-application-upgrade-data-serialization.md)
  * [신뢰할 수 있는 상태 관리자 구성](service-fabric-reliable-services-configuration.md)
* 기타
  * [Reliable Services 빠른 시작](service-fabric-reliable-services-quick-start.md)
  * [신뢰할 수 있는 컬렉션에 대한 개발자 참조](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
