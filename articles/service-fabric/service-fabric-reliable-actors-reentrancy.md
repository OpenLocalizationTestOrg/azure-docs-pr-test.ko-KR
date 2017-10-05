---
title: "행위자 기반 Azure 마이크로 서비스의 다시 표시 | Microsoft Docs"
description: "서비스 패브릭 Reliable Actors의 다시 표시에 대해 소개합니다."
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
ms.openlocfilehash: 00fcccb379bf1ba3875fbaba57a05b00fa228622
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="bd7ac-103">Reliable Actors 다시 표시</span><span class="sxs-lookup"><span data-stu-id="bd7ac-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="bd7ac-104">기본적으로 Reliable Actors 런타임을 사용하면 논리적 호출 컨텍스트를 기반으로 다시 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7ac-104">The Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="bd7ac-105">따라서 동일한 호출 컨텍스트 체인에 있는 경우 행위자가 다시 표시되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7ac-105">This allows for actors to be reentrant if they are in the same call context chain.</span></span> <span data-ttu-id="bd7ac-106">예를 들어 행위자 A가 행위자 C에 메시지를 보내는 행위자 B에 메시지를 보내는 경우 메시지 처리 과정의 일부로 행위자 C가 행위자 A를 호출하면 해당 메시지가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd7ac-106">For example, Actor A sends a message to Actor B, who sends a message to Actor C. As part of the message processing, if Actor C calls Actor A, the message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="bd7ac-107">다른 호출 컨텍스트의 일부인 다른 모든 메시지는 처리를 완료할 때까지 행위자 A에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd7ac-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="bd7ac-108">`ActorReentrancyMode` 열거에 정의된 행위자 다시 표시에 두 개의 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7ac-108">There are two options available for actor reentrancy defined in the `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="bd7ac-109">`LogicalCallContext` (기본 동작)</span><span class="sxs-lookup"><span data-stu-id="bd7ac-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="bd7ac-110">`Disallowed` - 다시 표시 비활성화</span><span class="sxs-lookup"><span data-stu-id="bd7ac-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="bd7ac-111">다시 표시는 등록하는 동안 `ActorService`의 설정에서 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7ac-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="bd7ac-112">행위자 서비스에서 만든 모든 행위자 인스턴스에 설정이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd7ac-112">The setting applies to all actor instances created in the actor service.</span></span>

<span data-ttu-id="bd7ac-113">다음 예제에서는 다시 표시 모드를 `ActorReentrancyMode.Disallowed`로 설정하는 행위자 서비스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd7ac-113">The following example shows an actor service that sets the reentrancy mode to `ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="bd7ac-114">이 경우, 행위자가 다시 표시 메시지를 다른 행위자에게 보내면 `FabricException` 형식의 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7ac-114">In this case, if an actor sends a reentrant message to another actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="bd7ac-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bd7ac-115">Next steps</span></span>
* <span data-ttu-id="bd7ac-116">[행위자 API 참조 설명서](https://msdn.microsoft.com/library/azure/dn971626.aspx)에서 재진입에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bd7ac-116">Learn more about reentrancy in the [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
