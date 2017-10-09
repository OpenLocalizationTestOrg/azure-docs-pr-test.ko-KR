---
title: "행위자 서비스 패브릭에서 aaaReliable | Microsoft Docs"
description: "Reliable Actors 신뢰할 수 있는 서비스에 계층화 하 고 hello 서비스 패브릭 플랫폼의 hello 기능을 사용 하는 방법에 대해 설명 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a><span data-ttu-id="e8c89-103">Reliable Actors hello 서비스 패브릭 플랫폼을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="e8c89-103">How Reliable Actors use hello Service Fabric platform</span></span>
<span data-ttu-id="e8c89-104">이 문서에서는 Reliable Actors hello Azure Service Fabric 플랫폼에서 작동 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-104">This article explains how Reliable Actors work on hello Azure Service Fabric platform.</span></span> <span data-ttu-id="e8c89-105">Reliable Actors hello를 호출 하는 신뢰할 수 있는 상태 저장 서비스의 구현에서 호스트 되는 프레임 워크에서 실행할 *행위자 서비스*합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called hello *actor service*.</span></span> <span data-ttu-id="e8c89-106">hello 행위자 서비스 모든 hello 구성 요소가 필요한 toomanage hello 수명 주기 및 디스패치 하 여 작업자에 대 한 메시지에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-106">hello actor service contains all hello components necessary toomanage hello lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="e8c89-107">hello 행위자 런타임, 가비지 수집 주기를 관리 하 고 단일 스레드 액세스를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-107">hello Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="e8c89-108">행위자 서비스 remoting 수신기 호출 tooactors 원격 액세스를 허용 하 고 tooa 발송자 tooroute toohello 적절 한 행위자 인스턴스에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-108">An actor service remoting listener accepts remote access calls tooactors and sends them tooa dispatcher tooroute toohello appropriate actor instance.</span></span>
* <span data-ttu-id="e8c89-109">행위자 상태 공급자 hello 상태 공급자 (예: hello 신뢰할 수 있는 컬렉션 상태 공급자)를 래핑하고 행위자 상태 관리에 대 한 어댑터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-109">hello Actor State Provider wraps state providers (such as hello Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="e8c89-110">이러한 구성 요소 구성 hello Reliable Actor 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-110">These components together form hello Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="e8c89-111">서비스 계층</span><span class="sxs-lookup"><span data-stu-id="e8c89-111">Service layering</span></span>
<span data-ttu-id="e8c89-112">Hello 행위자 서비스 자체는 신뢰할 수 있는 서비스 이므로 모든 hello [응용 프로그램 모델](service-fabric-application-model.md), 수명 주기 [패키징](service-fabric-package-apps.md), [배포](service-fabric-deploy-remove-applications.md), 업그레이드 및 개념의 크기 조정 신뢰할 수 있는 서비스는 hello 적용 tooactor 서비스 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-112">Because hello actor service itself is a reliable service, all hello [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply hello same way tooactor services.</span></span> 

![행위자 서비스 계층][1]

<span data-ttu-id="e8c89-114">hello 이전 다이어그램 관계를 보여 줍니다 hello hello 서비스 패브릭 응용 프로그램 프레임 워크와 사용자 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-114">hello preceding diagram shows hello relationship between hello Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="e8c89-115">파란색 요소 hello 신뢰할 수 있는 서비스 응용 프로그램 프레임 워크, 주황색 hello Reliable Actor 프레임 워크를 나타내는 나타내고 녹색 사용자 코드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-115">Blue elements represent hello Reliable Services application framework, orange represents hello Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="e8c89-116">신뢰할 수 있는 서비스에서 서비스는 hello 상속 `StatefulService` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-116">In Reliable Services, your service inherits hello `StatefulService` class.</span></span> <span data-ttu-id="e8c89-117">이 클래스는 `StatefulServiceBase`(또는 상태 비저장 서비스의 경우 `StatelessService`)에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="e8c89-118">Reliable Actors hello 행위자 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-118">In Reliable Actors, you use hello actor service.</span></span> <span data-ttu-id="e8c89-119">hello 행위자 서비스는 hello 다르게 구현 `StatefulServiceBase` 클래스에 작업 자가 실행 되는 위치는 구현 hello 행위자 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-119">hello actor service is a different implementation of hello `StatefulServiceBase` class that implements hello actor pattern where your actors run.</span></span> <span data-ttu-id="e8c89-120">Hello 행위자 서비스 자체의 구현을 뿐 이므로 `StatefulServiceBase`에서 파생 되는 서비스를 작성할 수 있습니다 `ActorService` 구현 서비스 수준의 기능이 동일 hello 및 상속 된 경우 동일한 방식으로 `StatefulService`, 같은:</span><span class="sxs-lookup"><span data-stu-id="e8c89-120">Because hello actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features hello same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="e8c89-121">서비스 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="e8c89-121">Service backup and restore.</span></span>
* <span data-ttu-id="e8c89-122">모든 행위자에 대한 공유 기능(예: 회로 차단기)</span><span class="sxs-lookup"><span data-stu-id="e8c89-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="e8c89-123">각 개별 행위자와 hello 행위자 서비스 자체에 원격 프로시저 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-123">Remote procedure calls on hello actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="e8c89-124">상태 저장 서비스는 현재 Java/Linux에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-hello-actor-service"></a><span data-ttu-id="e8c89-125">Hello 행위자 서비스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e8c89-125">Using hello actor service</span></span>
<span data-ttu-id="e8c89-126">행위자 인스턴스에 액세스 toohello 행위자 서비스를 실행 중인 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-126">Actor instances have access toohello actor service in which they are running.</span></span> <span data-ttu-id="e8c89-127">Hello 행위자 서비스를 통해 작업자 인스턴스 hello 서비스 컨텍스트를 프로그래밍 방식으로 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-127">Through hello actor service, actor instances can programmatically obtain hello service context.</span></span> <span data-ttu-id="e8c89-128">hello 서비스 컨텍스트는 hello 파티션 ID, 서비스 이름, 응용 프로그램 이름 및 기타 서비스 패브릭 플랫폼 관련 정보에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-128">hello service context has hello partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


<span data-ttu-id="e8c89-129">모든 신뢰할 수 있는 서비스와 마찬가지로 hello 서비스 패브릭 런타임에서 서비스 유형의으로 hello 행위자 서비스를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-129">Like all Reliable Services, hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="e8c89-130">Hello 행위자 toorun 작업자 인스턴스를 서비스, 행위자 형식 hello 행위자 서비스에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-130">For hello actor service toorun your actor instances, your actor type must also be registered with hello actor service.</span></span> <span data-ttu-id="e8c89-131">hello `ActorRuntime` 등록 메서드는 행위자를 위한이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-131">hello `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="e8c89-132">Hello 가장 간단한 경우에서 행위자 형식에만 등록할 수 있습니다 및 hello 행위자 서비스 기본 설정으로 암시적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-132">In hello simplest case, you can just register your actor type, and hello actor service with default settings will implicitly be used:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

<span data-ttu-id="e8c89-133">또는 hello 등록 메서드 tooconstruct hello 행위자 서비스에서 제공 하는 람다를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-133">Alternatively, you can use a lambda provided by hello registration method tooconstruct hello actor service yourself.</span></span> <span data-ttu-id="e8c89-134">다음 hello 행위자 서비스를 구성할 수 있고 명시적으로 생성자를 통해 종속성 tooyour 행위자 주입할 수 있는 사용자 행위자 인스턴스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-134">You can then configure hello actor service and explicitly construct your actor instances, where you can inject dependencies tooyour actor through its constructor:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a><span data-ttu-id="e8c89-135">행위자 서비스 메서드</span><span class="sxs-lookup"><span data-stu-id="e8c89-135">Actor service methods</span></span>
<span data-ttu-id="e8c89-136">행위자 서비스 구현 hello `IActorService` (C#) 또는 `ActorService` (Java) 다시 구현 하는 `IService` (C#) 또는 `Service` (Java 참조).</span><span class="sxs-lookup"><span data-stu-id="e8c89-136">hello Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="e8c89-137">서비스 메서드에 적용 원격 프로시저 호출을 허용 하는 신뢰할 수 있는 서비스 원격 작업에서 사용 하는 hello 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-137">This is hello interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="e8c89-138">원격 서비스를 통해 원격으로 호출할 수 있는 서비스 수준 메서드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="e8c89-139">행위자 열거</span><span class="sxs-lookup"><span data-stu-id="e8c89-139">Enumerating actors</span></span>
<span data-ttu-id="e8c89-140">hello 행위자 서비스는 클라이언트 hello 서비스를 호스팅하는 hello 작업자에 대 한 tooenumerate 메타 데이터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-140">hello actor service allows a client tooenumerate metadata about hello actors that hello service is hosting.</span></span> <span data-ttu-id="e8c89-141">Hello 행위자 서비스는 분할 된 상태 저장 서비스 이므로 열거형 파티션별로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-141">Because hello actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="e8c89-142">각 파티션에 여러 작업자 포함 될 수 있습니다, 때문에 hello 열거 하는 페이지 된 결과 집합으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-142">Because each partition might contain many actors, hello enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="e8c89-143">모든 페이지를 읽을 때까지 반복 하 여 hello 페이지 처리할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-143">hello pages are looped over until all pages are read.</span></span> <span data-ttu-id="e8c89-144">hello 방법을 예제와 다음 toocreate 행위자 서비스의 한 파티션에 있는 모든 활성 작업 자가 목록:</span><span class="sxs-lookup"><span data-stu-id="e8c89-144">hello following example shows how toocreate a list of all active actors in one partition of an actor service:</span></span>

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a><span data-ttu-id="e8c89-145">행위자 삭제</span><span class="sxs-lookup"><span data-stu-id="e8c89-145">Deleting actors</span></span>
<span data-ttu-id="e8c89-146">또한 hello 행위자 서비스 행위자를 삭제 하기 위한 함수가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-146">hello actor service also provides a function for deleting actors:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="e8c89-147">행위자와 해당 상태를 삭제에 대 한 자세한 내용은 참조 hello [행위자 주기 설명서](service-fabric-reliable-actors-lifecycle.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-147">For more information on deleting actors and their state, see hello [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="e8c89-148">사용자 지정 행위자 서비스</span><span class="sxs-lookup"><span data-stu-id="e8c89-148">Custom actor service</span></span>
<span data-ttu-id="e8c89-149">파생 되는 고유한 사용자 지정 행위자 서비스를 등록할 수 hello 행위자 등록 람다를 사용 하 여 `ActorService` (C#) 및 `FabricActorService` (Java 참조).</span><span class="sxs-lookup"><span data-stu-id="e8c89-149">By using hello actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="e8c89-150">이 사용자 지정 행위자 서비스에서 `ActorService`(C#) 또는 `FabricActorService`(Java)를 상속하는 서비스 클래스를 작성하여 고유한 서비스 수준 기능을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="e8c89-151">사용자 지정 행위자 서비스에서 모든 hello 행위자 런타임 기능을 상속 `ActorService` (C#) 또는 `FabricActorService` (Java) 서비스 메서드를 사용 하는 tooimplement를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-151">A custom actor service inherits all hello actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used tooimplement your own service methods.</span></span>

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
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
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="e8c89-152">행위자 백업 및 복원 구현</span><span class="sxs-lookup"><span data-stu-id="e8c89-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="e8c89-153">다음 예제는 hello, hello 사용자 지정 행위자 서비스를 노출 행위자 데이터를 메서드 tooback hello remoting 수신기에 이미 있는 이용 하 여 `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="e8c89-153">In hello following example, hello custom actor service exposes a method tooback up actor data by taking advantage of hello remoting listener already present in `ActorService`:</span></span>

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


<span data-ttu-id="e8c89-154">이 예제에서 `IMyActorService`은 `IService`(C#) 또는 `Service`(Java)를 구현하는 원격 계약이고 `MyActorService`에서 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="e8c89-155">이 원격 서비스 계약 메서드를 추가 하 여 `IMyActorService` 는 이제 사용 가능한 tooa 클라이언트를 통해 원격 프록시를 만들어 `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="e8c89-155">By adding this remoting contract, methods on `IMyActorService` are now also available tooa client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a><span data-ttu-id="e8c89-156">응용 프로그램 모델</span><span class="sxs-lookup"><span data-stu-id="e8c89-156">Application model</span></span>
<span data-ttu-id="e8c89-157">행위자 서비스 신뢰할 수 있는 서비스 되므로 hello 응용 프로그램 모델 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-157">Actor services are Reliable Services, so hello application model is hello same.</span></span> <span data-ttu-id="e8c89-158">그러나 hello 행위자 프레임 워크 빌드 도구 hello 응용 프로그램 모델 파일 중 일부를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-158">However, hello actor framework build tools generate some of hello application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="e8c89-159">서비스 매니페스트</span><span class="sxs-lookup"><span data-stu-id="e8c89-159">Service manifest</span></span>
<span data-ttu-id="e8c89-160">hello 행위자 프레임 워크 빌드 도구 행위자 서비스의 ServiceManifest.xml 파일의 내용을 hello를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-160">hello actor framework build tools automatically generate hello contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="e8c89-161">이 파일에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-161">This file includes:</span></span>

* <span data-ttu-id="e8c89-162">행위자 서비스 유형.</span><span class="sxs-lookup"><span data-stu-id="e8c89-162">Actor service type.</span></span> <span data-ttu-id="e8c89-163">hello 형식 이름은 행위자의 프로젝트 이름을 기반으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-163">hello type name is generated based on your actor's project name.</span></span> <span data-ttu-id="e8c89-164">행위자 사용자의 hello 지 속성 특성을 기반 hello HasPersistedState 플래그도에 따라 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-164">Based on hello persistence attribute on your actor, hello HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="e8c89-165">코드 패키지.</span><span class="sxs-lookup"><span data-stu-id="e8c89-165">Code package.</span></span>
* <span data-ttu-id="e8c89-166">구성 패키지.</span><span class="sxs-lookup"><span data-stu-id="e8c89-166">Config package.</span></span>
* <span data-ttu-id="e8c89-167">장치 및 끝점.</span><span class="sxs-lookup"><span data-stu-id="e8c89-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="e8c89-168">응용 프로그램 매니페스트.</span><span class="sxs-lookup"><span data-stu-id="e8c89-168">Application manifest</span></span>
<span data-ttu-id="e8c89-169">hello 행위자 프레임 워크 빌드 도구 행위자 서비스에 대 한 기본 서비스 정을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-169">hello actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="e8c89-170">hello 빌드 도구 hello 기본 서비스 속성을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-170">hello build tools populate hello default service properties:</span></span>

* <span data-ttu-id="e8c89-171">복제본 집합 수는 hello 지 속성 특성에 작업자에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-171">Replica set count is determined by hello persistence attribute on your actor.</span></span> <span data-ttu-id="e8c89-172">프로그램 행위자 각 시간 hello 지 속성 특성은 변경, hello 기본 서비스 정의에 hello 복제본 집합 수에 따라 다시 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-172">Each time hello persistence attribute on your actor is changed, hello replica set count in hello default service definition is reset accordingly.</span></span>
* <span data-ttu-id="e8c89-173">파티션 구성표와 범위 hello 전체 Int64 키 범위와 Int64 tooUniform 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-173">Partition scheme and range are set tooUniform Int64 with hello full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="e8c89-174">행위자에 대한 서비스 패브릭 파티션 개념</span><span class="sxs-lookup"><span data-stu-id="e8c89-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="e8c89-175">행위자 서비스는 분할된 상태 저장 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="e8c89-176">행위자 서비스의 각 파티션은 일련의 행위자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="e8c89-177">서비스 파티션은 서비스 패브릭에 있는 여러 노드에 자동으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="e8c89-178">결과적으로 행위자 인스턴스가 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-178">Actor instances are distributed as a result.</span></span>

![행위자 분할 및 배포][5]

<span data-ttu-id="e8c89-180">Reliable Services는 다른 파티션 구성표와 파티션 키 범위로 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="e8c89-181">hello 행위자 서비스는 hello 전체 Int64 키 범위 toomap 행위자 toopartitions 인 hello Int64 파티션 구성표를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-181">hello actor service uses hello Int64 partitioning scheme with hello full Int64 key range toomap actors toopartitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="e8c89-182">행위자 ID</span><span class="sxs-lookup"><span data-stu-id="e8c89-182">Actor ID</span></span>
<span data-ttu-id="e8c89-183">에 연결 된 hello를 나타내는 고유 ID hello 서비스에서 생성 된 각 행위자 `ActorId` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-183">Each actor that's created in hello service has a unique ID associated with it, represented by hello `ActorId` class.</span></span> <span data-ttu-id="e8c89-184">`ActorId`사용할 수 있는 작업자의 균일 한 분포에 대 한 hello 서비스 파티션 간에 임의의 Id를 생성 하 여는 불투명 ID 값:</span><span class="sxs-lookup"><span data-stu-id="e8c89-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across hello service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="e8c89-185">모든 `ActorId` 해시 된 tooan Int64 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-185">Every `ActorId` is hashed tooan Int64.</span></span> <span data-ttu-id="e8c89-186">이 때문에 hello 행위자 서비스 hello 전체 Int64 키 범위와 Int64 파티션 구성표를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-186">This is why hello actor service must use an Int64 partitioning scheme with hello full Int64 key range.</span></span> <span data-ttu-id="e8c89-187">그러나 사용자 지정 ID 값은 GUID/UUID, 문자열 및 Int64를 비롯한 `ActorID`에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

<span data-ttu-id="e8c89-188">Guid/Uuid 및 문자열을 사용 하는 hello 값은 해시 된 tooan Int64 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-188">When you're using GUIDs/UUIDs and strings, hello values are hashed tooan Int64.</span></span> <span data-ttu-id="e8c89-189">그러나 때 명시적으로 제공 Int64 tooan `ActorId`, Int64 hello 매핑됩니다 직접 tooa 파티션 없이 해시 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-189">However, when you're explicitly providing an Int64 tooan `ActorId`, hello Int64 will map directly tooa partition without further hashing.</span></span> <span data-ttu-id="e8c89-190">이 기술은 toocontrol 파티션 hello 행위자에 배치 되는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c89-190">You can use this technique toocontrol which partition hello actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8c89-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8c89-191">Next steps</span></span>
* [<span data-ttu-id="e8c89-192">행위자 상태 관리</span><span class="sxs-lookup"><span data-stu-id="e8c89-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="e8c89-193">행위자 수명 주기 및 가비지 수집</span><span class="sxs-lookup"><span data-stu-id="e8c89-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="e8c89-194">행위자 API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="e8c89-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="e8c89-195">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="e8c89-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="e8c89-196">Java 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="e8c89-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
