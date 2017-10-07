---
title: "aaaService 패브릭 신뢰할 수 있는 작업자 개요 | Microsoft Docs"
description: "소개 toohello 서비스 패브릭 Reliable Actors 프로그래밍 모델입니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 7fdad07f-f2d6-4c74-804d-e0d56131f060
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab010cbf936c6cf723b3d453ef95a9bf51f76c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-reliable-actors"></a>소개 tooService 패브릭 Reliable Actors
Reliable Actors hello에 따라 서비스 패브릭 응용 프로그램 프레임 워크는 [Virtual Actor](http://research.microsoft.com/en-us/projects/orleans/) 패턴입니다. 신뢰할 수 있는 작업자 API hello 서비스 패브릭에서 제공 hello 확장성 및 안정성 보장 기반 단일 스레드 프로그래밍 모델을 제공 합니다.

## <a name="what-are-actors"></a>행위자란?
행위자는 계산의 격리된 독립적인 단위이며 단일 스레드로 실행되는 상태입니다. hello [행위자 패턴](https://en.wikipedia.org/wiki/Actor_model) 동시 또는 분산 시스템에 있는 많은 수의 이러한 자 수 동시에 실행 하 고 서로 독립적으로 계산 모델입니다. 행위자는 서로 통신할 수 있으며 더 많은 행위자를 만들 수 있습니다.

### <a name="when-toouse-reliable-actors"></a>경우 Reliable Actors toouse
서비스 패브릭 Reliable Actors는 hello 행위자 디자인 패턴을 구현 합니다. 모든 소프트웨어 디자인 패턴에서와 마찬가지로 소프트웨어 문제를 디자인 하는 여부에 따라 toouse 특정 패턴은 있도록 하는지 여부를 결정을 hello hello 패턴을 적합 합니다.

Hello 행위자 디자인 패턴 잘 맞는 tooa 수가 분산된 시스템 문제 및 시나리오를 신중 하 게 수행 해야 하는 hello 패턴 및 구현 하는 hello 프레임 워크의 hello 제약 조건 고려 수 있습니다. 일반적인 지침으로 hello 행위자 패턴 toomodel 문제 또는 시나리오 경우 고려 합니다.

* 문제 영역은 1,000개 이상이라는 많은 수의 작고 독립적인 격리된 상태 및 논리 단위를 포함합니다.
* Toowork 행위자의 상태를 쿼리 등의 외부 구성 요소에서 중요 한 상호 작용 하지 않아도 되는 단일 스레드 개체와 함께 사용 하는 것이 좋습니다.
* 행위자 인스턴스는 I/O 작업을 실행하여 예측할 수 없는 지연으로 호출자를 차단하지 않습니다.

## <a name="actors-in-service-fabric"></a>서비스 패브릭의 행위자
서비스 패브릭 행위자 hello Reliable Actors 프레임 워크에서 구현 됩니다:는 행위자 패턴 기반 응용 프로그램 프레임 워크를 기반으로 구축 [서비스 패브릭 신뢰할 수 있는 서비스](service-fabric-reliable-services-introduction.md)합니다. 작성한 Reliable Actor 서비스는 각각 실제로 분할된 상태 저장 Reliable Service입니다.

동일한 toohello.NET 개체는 방식은.NET 형식의 인스턴스로 모든 행위자 행위자 형식의 인스턴스로 서 정의. 예를 들어 hello 기능 계산기를 구현 하는 행위자 형식 수 있으며 해당 형식의 다양 한 노드에서 클러스터를 통해 배포 되는 여러 작업자 있을 수 있습니다. 이러한 각 행위자는 행위자 ID에 의해 고유하게 식별됩니다.

### <a name="actor-lifetime"></a>행위자 수명
서비스 패브릭 행위자는 가상, 수명 동률된 tootheir 메모리 내 표현 되지 않음입니다. 결과적으로, 명시적으로 만들거나 제거할 toobe가 필요 하지 않습니다. hello Reliable Actors 런타임에서 자동으로 활성화 하는 행위자 hello 행위자 ID에 대 한 요청을 받은 처음으로 행위자 시간 동안 사용 하지 않으면, hello Reliable Actors 런타임 가비지-수집 hello 메모리 내 개체입니다. 또한 유지 합니다 hello 행위자의 존재 여부에 대 한 지식이 toobe 나중에 다시 활성화 해야 합니다. 자세한 내용은 [행위자 수명 주기 및 가비지 수집](service-fabric-reliable-actors-lifecycle.md)을 참조하세요.

이 가상 행위자 수명 추상화 hello 가상 행위자 모델의 결과로 서 몇 가지 주의할 사항이 생기고 실제로 hello Reliable Actors 구현에서에서 지나치게 벗어나는 시간에이 모델입니다.

* 행위자 (행위자 생성 개체 toobe 생김)를 자동으로 활성화 되어 hello 처음으로 메시지를 보내는 tooits 행위자 id입니다. 일부 시간이 지난 후 hello 행위자 개체가 가비지 수집입니다. Hello 생성 개체 toobe 앞으로 다시 hello 작업자 ID를 사용 하 여 새 작업자를 하면 됩니다. 행위자의 상태 hello 개체의 수명 더 이상 사용할 없는 hello 상태 관리자에 저장 합니다.
* 행위자 ID에 대한 행위자 메서드를 호출하면 해당 행위자를 활성화합니다. 이러한 이유로 행위자 형식에는 hello 런타임에 의해 암시적으로 호출의 생성자를 있습니다. 따라서 클라이언트 코드는 매개 변수 자체 hello 서비스에 의해 toohello 행위자 생성자 전달 될 수 있지만 매개 변수 toohello 행위자 형식의 생성자를 전달할 수 없습니다. hello 결과 행위자 생성할 수 있습니다. 부분적으로 초기화 상태에서, 다른 메서드가 호출 되기 hello 시간별 hello 행위자 hello 클라이언트에서 초기화 매개 변수를 요구 하는 경우입니다. Hello 클라이언트로부터 행위자의 hello 활성화에 대 한 단일 진입점이 있습니다.
* Reliable Actors 행위자 개체를 암시적으로 만들 있지만 사용자에 게는 행위자와 해당 상태를 삭제 하는 hello 기능 tooexplicitly.

### <a name="distribution-and-failover"></a>배포 및 장애 조치
서비스 패브릭 행위자 hello 클러스터 시킨다 고 자동으로 배포 tooprovide 확장성 및 안정성에서 필요에 따라 실패 한 노드 toohealthy 것으로 마이그레이션합니다. [분할된 상태 저장 Reliable Service](service-fabric-concepts-partitioning.md)에 대한 추상화합니다. 배포, 확장성, 안정성 및 자동 장애 조치가 모두 행위자 hello를 호출 하는 신뢰할 수 있는 상태 저장 서비스 내에서 실행 되는 hello 팩트에 의해 제공 됩니다 *행위자 서비스*합니다.

행위자 hello 행위자 서비스의 hello 파티션을 분산 되어 및 서비스 패브릭 클러스터의 hello 노드 간에 이러한 파티션을 분산 됩니다. 각 서비스 파티션은 일련의 행위자를 포함합니다. 서비스 패브릭 배포 및 장애 조치의 hello 서비스 파티션 관리합니다.

예를 들어 9 개의 파티션이 있는 행위자 서비스 배포 toothree hello 기본 행위자 파티션 배치를 사용 하 여 노드 다음과 같이 배포 합니다.

![Reliable Actors 분배][2]

hello 행위자 프레임 워크 사용자에 대 한 파티션 구성표와 키 범위 설정을 관리합니다. 이는 일부 선택을 간소화하지만 다음과 같은 몇 가지를 고려해야 합니다.

* 신뢰할 수 있는 서비스 toochoose 파티션 구성표 (범위 파티션 구성표를 사용 하 여) 하는 경우 키 범위 있으며 파티션을 계산 합니다. Reliable Actors 제한 toohello 범위 파티션 구성표 (균일 Int64 구성표 hello) 이며 hello 전체 Int64 키 범위를 사용 하 여이 필요 합니다.
* 기본적으로 행위자는 균일하게 분포되는 파티션에 임의로 배치됩니다.
* 행위자가 임의로 배치되기 때문에 행위자 작업은 메서드 호출 데이터의 직렬화 및 역직렬화를 포함하여 네트워크 통신이 항상 필요하며 이는 대기 시간 및 오버헤드를 발생시킨다는 점을 예상해야 합니다.
* 고급 시나리오에서는 Int64 행위자 toospecific 파티션을 매핑하는 Id를 사용 하 여 가능한 toocontrol 행위자 파티션에 배치 됩니다. 그러나 이렇게 하면 파티션에 행위자를 불균형하게 배치하게 될 수 있습니다.

행위자 서비스 분할 되는 방식에 대 한 자세한 내용은 참조 너무[작업자에 대 한 개념을 분할](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors)합니다.

### <a name="actor-communication"></a>행위자 통신
행위자 상호 작용은 hello 인터페이스를 구현 하는 hello 행위자 및 프록시 tooan 행위자 hello 통해 가져오는 hello 클라이언트에서 공유 하는 인터페이스에 정의 된 동일한 인터페이스입니다. 이 인터페이스는 비동기적으로 사용 되는 tooinvoke 행위자 방법, 되므로 hello 인터페이스에서 모든 메서드 작업 반환 해야 합니다.

메서드 호출 대 한 응답을 수행 하면 결국 네트워크 요청 hello 클러스터, 따라서 hello 인수 및 반환 hello 플랫폼에 따라 직렬화 해야 하는 hello 작업의 결과 형식을 hello에 걸쳐 있습니다. 특히, [데이터 계약 직렬화가 가능](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)해야 합니다.

#### <a name="hello-actor-proxy"></a>hello 행위자 프록시
hello Reliable Actors 클라이언트 API 행위자 인스턴스 및 행위자 클라이언트 간의 통신을 제공 합니다. 행위자와 toocommunicate, 클라이언트 hello 행위자 인터페이스를 구현 하는 행위자 프록시 개체를 만듭니다. hello 클라이언트 hello 프록시 개체에 메서드를 호출 하 여 hello 행위자 상호 작용합니다. 클라이언트-행위자 및 행위자 행위자 통신에 대 한 hello 행위자 프록시를 사용할 수 있습니다.

```csharp
// Create a randomly distributed actor ID
ActorId actorId = ActorId.CreateRandom();

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
IMyActor myActor = ActorProxy.Create<IMyActor>(actorId, new Uri("fabric:/MyApp/MyActorService"));

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
await myActor.DoWorkAsync();
```

```java
// Create actor ID with some name
ActorId actorId = new ActorId("Actor1");

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
MyActor myActor = ActorProxyBase.create(actorId, new URI("fabric:/MyApp/MyActorService"), MyActor.class);

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
myActor.DoWorkAsync().get();
```


Hello 두 가지 정보 toocreate hello 행위자 프록시 개체는 사용은 hello 작업자 ID 및 hello 응용 프로그램 이름입니다. hello 작업자 ID는 고유 하 게 hello 행위자를 식별 hello 응용 프로그램 이름은 hello를 식별 하는 동안 [서비스 패브릭 응용 프로그램](service-fabric-reliable-actors-platform.md#application-model) hello 행위자 배포 되는 위치입니다.

hello `ActorProxy`(C#) / `ActorProxyBase`hello 클라이언트 쪽에서 (Java) 클래스 ID 별로 hello 필요한 해상도 toolocate hello 행위자를 수행 하 고 함께 통신 채널을 열립니다. 또한 toolocate hello 행위자 통신 오류 및 장애 조치의 경우 hello에에서 다시 시도합니다. 결과적으로, 메시지 배달 hello 특성 뒤에 있습니다.

* 메시지 전달은 최선을 다합니다.
* 행위자 hello에서 중복 된 메시지를 받을 수 동일한 클라이언트입니다.

### <a name="concurrency"></a>동시성
hello Reliable Actors 런타임은 행위자 메서드에 액세스 하기 위한 간단한 턴 기반 액세스 모델을 제공 합니다. 따라서 행위자 개체의 코드 내에는 항상 둘 이상의 스레드가 활성화될 수 없습니다. 데이터 액세스에 대한 동기화 메커니즘이 필요하지 않기에 턴 기반 액세스는 동시 시스템을 매우 간소화합니다. 또한 각 행위자 인스턴스의 hello 단일 스레드 액세스 특성에 대 한 특별 한 고려 사항 시스템을 디자인 해야 의미 합니다.

* 단일 행위자 인스턴스는 한 번에 둘 이상의 요청을 처리할 수 없습니다. 동시 요청 수가 예상된 toohandle는 행위자 인스턴스 처리량 병목 지점이 발생할 수 있습니다.
* 하면서 외부 요청은 hello 작업자 tooone 동시에 두 명의 작업자 서로 순환 요청 하는 경우 행위자는 서로 교착 상태가 발생할 수 있습니다. hello 행위자 런타임은 행위자에서 시간에 자동으로 호출 하 고 교착 상태가 발생할 예외 toohello 호출자 toointerrupt을 throw 합니다.

![Reliable Actors 통신][3]

#### <a name="turn-based-access"></a>턴 기반 액세스
다른 행위자 또는 클라이언트에서 응답 tooa 요청에서 행위자 메서드의 실행 완료 hello 또는 hello의 실행 완료 순서 대로 구성 되어는 [타이머/미리 알림](service-fabric-reliable-actors-timers-reminders.md) 콜백 합니다. 이러한 메서드와 콜백이 비동기 인 경우에 hello 행위자 런타임을 인터리브 하지 않습니다. 하나의 턴을 완전히 완료해야 새로운 턴이 허용됩니다. 즉, 현재 실행 하는 행위자 메서드 또는 타이머/미리 알림 콜백을 완전히 새 tooa 메서드 호출 하기 전에 완료 해야 합니다. 또는 콜백 ï ´ ù. 메서드 또는 콜백으로 간주 됩니다 toohave 완성 된 hello 실행 hello 메서드에서 반환 되는 또는 hello 메서드 또는 콜백에서 반환 된 콜백 및 hello 작업을 마쳤습니다. 서로 다른 메서드, 타이머 및 콜백 전체에 걸쳐 턴 기반 동시성이 준수된다는 것을 강조할 가치가 있습니다.

hello 행위자 런타임에서 턴 기반 동시성을 순서 대로 hello 맨 앞에 행위자 별 잠금을 확보 하 여 적용 하 고 전원을 hello hello 끝나기 전에 hello 잠금을 해제 합니다. 따라서 행위자들 전체가 아닌 각각의 행위자 단위로 턴 기반 동시성이 적용됩니다. 행위자 메서드와 타이머/미리 알림 콜백은 여러 행위자를 대신하여 동시에 실행할 수 있습니다.

다음 예제는 hello를 hello를 위에 개념을 보여 줍니다. 두 비동기 메서드(즉, *Method1* 및 *Method2*), 타이머 및 미리 알림을 구현하는 행위자 형식을 고려합니다. 아래 hello 다이어그램 두 행위자를 대신 하 여 이러한 메서드와 콜백을의 hello 실행에 대 한 타임 라인의 예를 보여 줍니다 (*ActorId1* 및 *ActorId2*) 속하는 toothis 행위자 형식입니다.

![Reliable Actors 런타임 턴 기반 동시성 및 액세스][1]

이 다이어그램은 다음 규칙을 따릅니다.

* 각 세로선 hello 논리 특정 행위자를 대신 하 여 메서드 또는 콜백을 실행 흐름을 보여 줍니다.
* 각 세로 줄에 표시 된 hello 이벤트 시간 순서 대로 이전 기능 아래 발생 하는 최신 이벤트를 발생 합니다.
* 서로 다른 색 toodifferent 행위자를 해당 하는 타임 라인에 사용 됩니다.
* 강조 표시는 hello에 대 한 메서드 또는 콜백을 대신 하 여 행위자 별 잠금을 얻기 커서가 사용 되는 tooindicate hello 기간입니다.

몇 가지 중요 한 사항 tooconsider:

* 반면 *Method1* 대신 실행 *ActorId2* tooclient 요청 응답에에서 *xyz789*, 다른 클라이언트 요청 (*abc123*) 메시지가 도착 하면도 필요 *Method1* 에 의해 실행 toobe *ActorId2*합니다. 그러나 두 번째로 실행 hello *Method1* hello 이전 실행이 끝날 때까지 시작 되지 않습니다. 에 의해 미리 알림을 등록 하는 마찬가지로, *ActorId2* 발생 하는 동안 *Method1* 응답 tooclient 요청에서 실행 중인 *xyz789*합니다. hello 미리 알림 콜백이 실행의 두 실행 한 후에 *Method1* 완료 됩니다. 이 작업이 모두에 대해 적용 되 고 tooturn 기반 동시성 인해 *ActorId2*합니다.
* 마찬가지로, 턴 기반 동시성도 적용 *ActorId1*hello 실행 하 여 볼 수 있듯이, *Method1*, *Method2*를 대신 하 여 타이머 콜백 hello 및 *ActorId1* 순차적으로 발생 합니다.
* *ActorId1*을 대신한 *Method1*의 실행은 *ActorId2*를 대신한 실행과 겹칩니다. 이는 턴 기반 동시성이 전체 행위자들이 아닌 하나의 행위자 내에만 적용되기 때문입니다.
* 일부 hello 메서드/콜백 실행의 hello `Task`(C#) / `CompletableFuture`hello 메서드에서 반환 된 후 (Java) hello 메서드/콜백 완료 하 여 반환 합니다. 일부 다른 hello 비동기 작업이 이미 완료 되었습니다 hello 시간별 hello 메서드/콜백이 반환 합니다. 두 경우 모두 hello 행위자 별 잠금은 모두 hello 메서드/콜백이 반환 하 고 hello 비동기 작업이 완료 된 후에 해제 됩니다.

#### <a name="reentrancy"></a>다시 표시
hello 행위자 런타임 기본적으로 재진입을 수 있습니다. 즉는 행위자 방법을 *행위자 A* 에서 메서드를 호출 *행위자 B*를 호출 하 여 다른 방법에 *행위자 A*, 메서드는 toorun를 허용 합니다. 이 hello의 일부 이기 때문에 동일한 논리 호출 체인 컨텍스트입니다. 모든 타이머 및 미리 알림을 호출 새 논리 호출 컨텍스트의 hello로 시작합니다. Hello 참조 [Reliable Actors 재진입](service-fabric-reliable-actors-reentrancy.md) 자세한 세부 정보에 대 한 합니다.

#### <a name="scope-of-concurrency-guarantees"></a>동시성 보증의 범위
hello 행위자 런타임은 이러한 메서드의 hello 호출을 제어 하는 경우에 이러한 동시성 보증을 제공 합니다. 예를 들어 타이머 및 미리 알림 콜백이 뿐만 아니라 응답 tooa 클라이언트 요청에서 수행 하는 hello 메서드 호출에 대해 이러한 보증 제공 합니다. 그러나 hello 행위자 코드 hello 행위자 런타임에서 제공 하는 hello 메커니즘 외부에서 이러한 메서드를 직접 호출 후 hello 런타임 제공할 수 없는 경우 동시성 보장은 합니다. 예를 들어 hello 행위자 메서드에 의해 반환 되는 hello 태스크와 연결 되지 않은 일부 작업의 hello 컨텍스트에서 hello 메서드가 호출 되 면 다음 hello 런타임 제공할 수 없는 경우 동시성 보장 합니다. Hello 메서드 스레드에서 호출 하는 경우 해당 hello 배우는 자체적으로 만든 다음 hello 런타임도 제공할 수 없습니다 동시성 보장 합니다. 따라서 tooperform 백그라운드 작업 작업자를 사용 해야 [행위자 타이머 및 행위자 미리](service-fabric-reliable-actors-timers-reminders.md) 턴 기반 동시성을 준수 하는 합니다.

## <a name="next-steps"></a>다음 단계
* 첫 번째 Reliable Actors 서비스를 빌드하여 시작합니다.
   * [.NET에서 Reliable Actors 시작](service-fabric-reliable-actors-get-started.md)
   * [Java에서 Reliable Actors 시작](service-fabric-reliable-actors-get-started-java.md)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-introduction/concurrency.png
[2]: ./media/service-fabric-reliable-actors-introduction/distribution.png
[3]: ./media/service-fabric-reliable-actors-introduction/actor-communication.png
