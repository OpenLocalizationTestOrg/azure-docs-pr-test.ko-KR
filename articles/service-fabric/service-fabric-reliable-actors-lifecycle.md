---
title: "Azure microservices 행위자 기반 수명 주기의 aaaOverview | Microsoft Docs"
description: "서비스 패브릭 Reliable Actor 수명 주기, 가비지 수집 및 행위자와 해당 상태 수동 삭제에 대해 설명합니다."
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a>행위자 수명 주기, 자동 가비지 수집 및 수동 삭제
행위자가 활성화 hello 처음으로 tooany 메서드 호출 합니다. 행위자 비활성화 (가비지 수집된 hello 행위자 런타임에서) 이면 구성 가능한 일정 시간 동안에는 사용 되지 않습니다. 행위자와 그 상태를 언제든지 수동으로 삭제할 수도 있습니다.

## <a name="actor-activation"></a>행위자 활성화
행위자가 활성화 hello 다음 작업이 수행 됩니다.

* 행위자를 호출하는 경우 아직 활성화되지 않았으면 새 행위자를 만듭니다.
* 상태를 유지 하는 경우 hello 행위자의 상태가 로드 됩니다.
* hello `OnActivateAsync` (C#) 또는 `onActivateAsync` (있음 hello 행위자 구현에서 재정의할 수 있음) (Java) 메서드를 호출 합니다.
* 이제 hello 행위자 활성 간주 됩니다.

## <a name="actor-deactivation"></a>행위자 비활성화
행위자 비활성화 되 면 hello 다음 작업이 수행 됩니다.

* 행위자 일정 기간을 사용 하지 않으면 hello 활성 작업자 테이블에서 제거 됩니다.
* hello `OnDeactivateAsync` (C#) 또는 `onDeactivateAsync` (있음 hello 행위자 구현에서 재정의할 수 있음) (Java) 메서드를 호출 합니다. Hello 작업자에 대해 모든 hello 타이머를 지웁니다. 상태 변경과 같은 행위자 작업은 이 메서드에서 호출되지 않습니다.

> [!TIP]
> hello 패브릭 행위자 런타임에서 내보내는 일부 [tooactor 활성화 및 비활성화와 관련 된 이벤트](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters)합니다. 진단 및 성능 모니터링에 유용합니다.
>
>

### <a name="actor-garbage-collection"></a>행위자 가비지 수집
행위자 비활성화 되 면 toohello 행위자 개체를 참조 해제 되 고 hello 공용 언어 런타임 (CLR) 또는 java 가상 컴퓨터 (JVM) 가비지 수집기에서 일반적으로 수집 수 있습니다. 가비지 수집만 hello 행위자 개체를 정리 그렇게 **하지** hello 행위자 상태 관리자에 저장 된 상태가 제거 합니다. hello 다음 시간 hello 행위자가 활성화 하 고 새 행위자 개체를 만드는 상태로 복원 됩니다.

"사용"을 비활성화 및 가비지 수집 hello 목적으로 계산 하는 무엇입니까?

* 호출 수신
* `IRemindable.ReceiveReminderAsync`메서드 호출 (hello 행위자 미리 알림을 사용 하는 경우에 해당)

> [!NOTE]
> hello 행위자 타이머를 사용 하 여 해당 타이머 콜백이 호출 되는 경우 그렇게 **하지** "사용"로 계산 합니다.
>
>

비활성화의 hello 자세히 살펴보기 전에 것이 중요 한 toodefine hello 아래 계약 내용:

* *스캔 간격*. 이 hello 행위자에서 런타임 비활성화 될 수 있는 작업자에 대 한 해당 활성 작업자 테이블을 검색 하는 hello 간격 이므로 가비지가 수집 합니다. 이 대 한 hello 기본값은 1 분입니다.
* *유휴 시간 제한*. 이 hello 시간 행위자 필요 함을 tooremain 사용 되지 않는 가비지가 수집 하 고 비활성화할 수 있습니다 (유휴 상태). 이 대 한 hello 기본값은 60 분입니다.

일반적으로 불필요 toochange이이 기본값입니다. 그러나 [행위자 서비스](service-fabric-reliable-actors-platform.md)를 등록할 때 필요한 경우 `ActorServiceSettings`를 통해 이러한 간격을 변경할 수 있습니다.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
    }
}
```

```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
    }
}
```
각 활성 작업자에 대해 hello 행위자 런타임은 hello 총 시간이 경과 했는데도 문제가 있다면 유휴 상태 (사용 되지 않은)의 추적 합니다. hello 행위자 런타임 검사 각각 hello 행위자의 모든 `ScanIntervalInSeconds` 가비지 수 있으면 toosee 수집 하 고 경우에 대 한 유휴 상태 수집 `IdleTimeoutInSeconds`합니다.

행위자 사용 하는 경우 언제 든 지 고 유휴 시간 재설정 too0입니다. 그러면 hello 행위자 다시 유휴 상태로 대기에 대 한 경우에 가비지 수집 될 수 있습니다 `IdleTimeoutInSeconds`합니다. 행위자 toohave 것으로 간주 됩니다 회수 된 행위자 인터페이스 메서드 또는 행위자 미리 알림 콜백이 실행 되는 경우 사용 합니다. 자가 **하지** toohave 것으로 간주 되어 해당 타이머 콜백이 실행 되는 경우 사용 합니다.

hello 다음 다이어그램에서는 단일 행위자 tooillustrate의 hello 수명 주기 이러한 개념

![유휴 시간의 예][1]

hello 예제에는이 행위자의 lifetime hello에 행위자 메서드 호출, 알림과 타이머의 hello 영향을 보여 줍니다. hello hello 예에 대 한 포인트 다음은 주의 해야 합니다.

* ScanInterval 및 IdleTimeout too5 및 10는 각각 설정 됩니다. (단위 않습니다 중요 하지 여기에서는 이러한 목적에만 tooillustrate hello 개념 이므로.)
* hello 검색 간격을 5에 정의 된 대로 toobe 가비지 수집 T = 0, 5, 10, 15, 20, 25에서 발생 하는 행위자를 위한 hello 검색 합니다.
* 주기적 타이머는 T=4,8,12,16,20,24에서 발생하며 해당 콜백이 실행됩니다. Hello hello 행위자의 유휴 시간을 영향을 주지 않습니다.
* T = 7에는 행위자 메서드 호출 hello 유휴 시간 too0을 hello 행위자의 hello 가비지 컬렉션을 지연 합니다.
* T = 14에서 행위자 미리 알림 콜백을 실행 하 고 추가 지연이 hello hello 행위자의 가비지 수집 키를 누릅니다.
* T = 25 hello 가비지 컬렉션 검사 수행 hello 행위자의 유휴 시간은 마지막으로 10 hello 유휴 시간 제한을 초과 하 고 hello 행위자가 가비지 수집 합니다.

메서드 중 하나를 실행하는 동안에는 해당 메서드를 실행하는 데 소요되는 시간에 상관 없이 행위자는 절대 가비지 수집되지 않습니다. 앞서 언급 했 듯이 행위자 인터페이스 메서드 및 미리 알림 콜백을 실행 hello hello 행위자의 유휴 시간 too0 다시 설정 하 여 가비지 수집을 방지 합니다. 타이머 콜백 실행 hello hello 유휴 시간 too0를 설정 하지 않습니다. 그러나 hello 행위자의 가비지 수집을 hello hello 타이머 콜백을 실행이 완료 될 때까지 지연 됩니다.

## <a name="deleting-actors-and-their-state"></a>행위자와 해당 상태 삭제
비활성화 된 작업자의 가비지 수집만 hello 행위자 개체를 정리 하지만 행위자의 상태 관리자에 저장 된 데이터는 제거 되지 않습니다. 행위자 다시 활성화 되 면 해당 데이터 hello 상태 관리자를 통해 사용할 수 있는 tooit은 다시 설정 됩니다. 여기서 행위자 상태 관리자에 데이터를 저장 하 고 비활성화 있지만 되지 다시 활성화의 경우에서 해당 데이터를 필요한 tooclean 수도 있습니다.

hello [행위자 서비스](service-fabric-reliable-actors-platform.md) 원격 호출자에서 작업자를 삭제 하기 위한 함수를 제공 합니다.

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

작업자 삭제 효과 hello 행위자 현재 활성 인지 아닌지에 따라 다음 hello에 있습니다.

* **활성 행위자**
  * 행위자가 활성 행위자 목록에서 제거되고 비활성화됩니다.
  * 해당 상태가 영구적으로 삭제됩니다.
* **비활성 행위자**
  * 해당 상태가 영구적으로 삭제됩니다.

행위자를 호출할 수 없습니다는 런타임은 hello 행위자 호출 tooenforce 단일 스레드 액세스 잠금을 hello에서 확보 하는 행위자 호출 컨텍스트 내에서 실행 하는 동안 hello 행위자를 삭제할 수 없으므로 행위자 메서드 중 하나에서 자체에서 삭제 합니다.

## <a name="next-steps"></a>다음 단계
* [행위자 타이머 및 미리 알림](service-fabric-reliable-actors-timers-reminders.md)
* [행위자 이벤트](service-fabric-reliable-actors-events.md)
* [행위자 다시 표시](service-fabric-reliable-actors-reentrancy.md)
* [행위자 진단 및 성능 모니터링](service-fabric-reliable-actors-diagnostics.md)
* [행위자 API 참조 설명서](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [C# 샘플 코드](https://github.com/Azure/servicefabric-samples)
* [Java 샘플 코드](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
