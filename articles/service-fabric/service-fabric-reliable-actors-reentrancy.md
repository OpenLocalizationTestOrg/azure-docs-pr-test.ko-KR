---
title: "Azure microservices 행위자 기반에서 aaaReentrancy | Microsoft Docs"
description: "서비스 패브릭 Reliable Actors에 대 한 소개 tooreentrancy"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="3c14a-103">Reliable Actors 다시 표시</span><span class="sxs-lookup"><span data-stu-id="3c14a-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="3c14a-104">기본적으로 hello Reliable Actors 런타임 논리 호출 컨텍스트에 기반 재진입을 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c14a-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="3c14a-105">이 통해 행위자 toobe reentrant hello에 있는 경우 동일한 상황에 맞는 체인을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c14a-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="3c14a-106">예를 들어 A 행위자가 보냅니다 메시지 tooActor 3. 보내는 메시지 tooActor B Hello 메시지 처리의 일부로 행위자 C는 A, 행위자를 호출 하는 경우 hello 메시지 이므로 재진입 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c14a-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="3c14a-107">다른 호출 컨텍스트의 일부인 다른 모든 메시지는 처리를 완료할 때까지 행위자 A에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c14a-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="3c14a-108">Hello에 정의 된 행위자 재입력에 사용할 수 있는 옵션 두 가지가 `ActorReentrancyMode` enum:</span><span class="sxs-lookup"><span data-stu-id="3c14a-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="3c14a-109">`LogicalCallContext` (기본 동작)</span><span class="sxs-lookup"><span data-stu-id="3c14a-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="3c14a-110">`Disallowed` - 다시 표시 비활성화</span><span class="sxs-lookup"><span data-stu-id="3c14a-110">`Disallowed` - disables reentrancy</span></span>

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
<span data-ttu-id="3c14a-111">다시 표시는 등록하는 동안 `ActorService`의 설정에서 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c14a-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="3c14a-112">hello 설정은 hello 행위자 서비스에서 만든 tooall 행위자 인스턴스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c14a-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="3c14a-113">hello 다음 보여 주는 예제 너무 hello 재진입 모드를 설정 하는 행위자 서비스`ActorReentrancyMode.Disallowed`합니다.</span><span class="sxs-lookup"><span data-stu-id="3c14a-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="3c14a-114">이 경우 행위자 재진입 메시지 tooanother 행위자 형식의 예외를 보내는 경우 `FabricException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c14a-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="3c14a-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c14a-115">Next steps</span></span>
* <span data-ttu-id="3c14a-116">재진입 hello에 대 한 자세한 [행위자 API 참조 설명서](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="3c14a-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
