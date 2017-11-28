---
title: "Service Fabric의 Reliable Actors| Microsoft Docs"
description: "Reliable Actors를 Reliable Services에 계층화하고 서비스 패브릭 플랫폼의 기능을 사용하는 방법을 설명합니다."
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
ms.openlocfilehash: 0a12da52b6e74c721cd25f89e7cde3c07153a396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-reliable-actors-use-the-service-fabric-platform"></a><span data-ttu-id="b8a9b-103">신뢰할 수 있는 행위자가 서비스 패브릭 플랫폼을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b8a9b-103">How Reliable Actors use the Service Fabric platform</span></span>
<span data-ttu-id="b8a9b-104">이 문서에서는 Azure Service Fabric 플랫폼에서 Reliable Actors가 작동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-104">This article explains how Reliable Actors work on the Azure Service Fabric platform.</span></span> <span data-ttu-id="b8a9b-105">Reliable Actors는 *행위자 서비스*라는 상태 저장 신뢰할 수 있는 서비스의 구현에서 호스트되는 프레임워크에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called the *actor service*.</span></span> <span data-ttu-id="b8a9b-106">행위자 서비스는 행위자에게 발송되는 수명 주기 및 메시지를 관리하는 데 필요한 모든 구성 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-106">The actor service contains all the components necessary to manage the lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="b8a9b-107">행위자 런타임은 수명 주기, 가비지 수집을 관리하고 단일 스레드 액세스를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-107">The Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="b8a9b-108">행위자 서비스 원격 수신기는 행위자에 대한 원격 액세스 호출을 허용하고 적절한 행위자 인스턴스를 라우팅하는 디스패처에게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-108">An actor service remoting listener accepts remote access calls to actors and sends them to a dispatcher to route to the appropriate actor instance.</span></span>
* <span data-ttu-id="b8a9b-109">행위자 상태 제공자는 상태 공급자(예: 신뢰할 수 있는 컬렉션 상태 공급자)를 래핑하고 행위자 상태 관리에 대한 어댑터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-109">The Actor State Provider wraps state providers (such as the Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="b8a9b-110">이러한 구성 요소는 Reliable Actor 프레임워크를 함께 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-110">These components together form the Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="b8a9b-111">서비스 계층</span><span class="sxs-lookup"><span data-stu-id="b8a9b-111">Service layering</span></span>
<span data-ttu-id="b8a9b-112">행위자 서비스 자체가 Reliable Service이므로 Reliable Services의 [응용 프로그램 모델](service-fabric-application-model.md), 수명 주기, [패키징](service-fabric-package-apps.md), [배포](service-fabric-deploy-remove-applications.md), 업그레이드 및 개념 확장은 모두 행위자 서비스에 동일한 방식으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-112">Because the actor service itself is a reliable service, all the [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply the same way to actor services.</span></span> 

![행위자 서비스 계층][1]

<span data-ttu-id="b8a9b-114">이전 다이어그램은 Service Fabric 응용 프로그램 프레임워크와 사용자 코드 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-114">The preceding diagram shows the relationship between the Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="b8a9b-115">블루 요소는 Reliable Services 응용 프로그램 프레임워크를 나타내고 오렌지는 Reliable Actor 프레임워크를 나타내며 그린은 사용자 코드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-115">Blue elements represent the Reliable Services application framework, orange represents the Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="b8a9b-116">Reliable Services에서 서비스는 `StatefulService` 클래스를 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-116">In Reliable Services, your service inherits the `StatefulService` class.</span></span> <span data-ttu-id="b8a9b-117">이 클래스는 `StatefulServiceBase`(또는 상태 비저장 서비스의 경우 `StatelessService`)에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="b8a9b-118">Reliable Actors에서 행위자 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-118">In Reliable Actors, you use the actor service.</span></span> <span data-ttu-id="b8a9b-119">행위자 서비스는 행위자가 실행되는 행위자 패턴을 구현하는 `StatefulServiceBase` 클래스의 다른 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-119">The actor service is a different implementation of the `StatefulServiceBase` class that implements the actor pattern where your actors run.</span></span> <span data-ttu-id="b8a9b-120">행위자 서비스 자체는 `StatefulServiceBase`의 구현이므로 `ActorService`에서 파생된 고유한 서비스를 작성할 수 있고 다음과 같이 `StatefulService`을 상속하는 경우와 동일한 방식으로 서비스 수준 기능을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-120">Because the actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features the same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="b8a9b-121">서비스 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="b8a9b-121">Service backup and restore.</span></span>
* <span data-ttu-id="b8a9b-122">모든 행위자에 대한 공유 기능(예: 회로 차단기)</span><span class="sxs-lookup"><span data-stu-id="b8a9b-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="b8a9b-123">행위자 서비스 자체 및 각 개별 행위자에서의 원격 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="b8a9b-123">Remote procedure calls on the actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="b8a9b-124">상태 저장 서비스는 현재 Java/Linux에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-the-actor-service"></a><span data-ttu-id="b8a9b-125">행위자 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="b8a9b-125">Using the actor service</span></span>
<span data-ttu-id="b8a9b-126">행위자 인스턴스는 실행 중인 행위자 서비스에 대한 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-126">Actor instances have access to the actor service in which they are running.</span></span> <span data-ttu-id="b8a9b-127">행위자 인스턴스는 행위자 서비스를 통해 프로그래밍 방식으로 서비스 컨텍스트를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-127">Through the actor service, actor instances can programmatically obtain the service context.</span></span> <span data-ttu-id="b8a9b-128">서비스 컨텍스트에는 파티션 ID, 서비스 이름, 응용 프로그램 이름 및 기타 Service Fabric 플랫폼 관련 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-128">The service context has the partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

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


<span data-ttu-id="b8a9b-129">Reliable Services처럼 행위자 서비스는 Service Fabric 런타임에서 서비스 유형으로 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-129">Like all Reliable Services, the actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="b8a9b-130">행위자 인스턴스를 실행하는 행위자 서비스의 경우 행위자 서비스에 행위자 유형이 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-130">For the actor service to run your actor instances, your actor type must also be registered with the actor service.</span></span> <span data-ttu-id="b8a9b-131">`ActorRuntime` 등록 메서드가 행위자에 대한 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-131">The `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="b8a9b-132">가장 간단한 경우 행위자 형식만을 등록할 수 있고 기본 설정이 있는 행위자 서비스는 암시적으로 다음과 같은 경우 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-132">In the simplest case, you can just register your actor type, and the actor service with default settings will implicitly be used:</span></span>

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

<span data-ttu-id="b8a9b-133">또는 행위자 서비스를 직접 생성하는 등록 메서드가 제공하는 람다를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-133">Alternatively, you can use a lambda provided by the registration method to construct the actor service yourself.</span></span> <span data-ttu-id="b8a9b-134">그런 다음 생성자를 통해 행위자에 종속성을 주입할 수 있는 행위자 인스턴스를 명시적으로 생성하고 행위자 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-134">You can then configure the actor service and explicitly construct your actor instances, where you can inject dependencies to your actor through its constructor:</span></span>

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

### <a name="actor-service-methods"></a><span data-ttu-id="b8a9b-135">행위자 서비스 메서드</span><span class="sxs-lookup"><span data-stu-id="b8a9b-135">Actor service methods</span></span>
<span data-ttu-id="b8a9b-136">행위자 서비스는 `IActorService`(C#) 또는 `ActorService`(Java)를 구현하며 이는 `IService`(C#) 또는 `Service`(Java)를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-136">The Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="b8a9b-137">그러면 원격 서비스 메서드에서 프로시저 호출을 허용하지 않는 Reliable Services 원격 서비스에서 사용되는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-137">This is the interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="b8a9b-138">원격 서비스를 통해 원격으로 호출할 수 있는 서비스 수준 메서드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="b8a9b-139">행위자 열거</span><span class="sxs-lookup"><span data-stu-id="b8a9b-139">Enumerating actors</span></span>
<span data-ttu-id="b8a9b-140">행위자 서비스를 사용하면 클라이언트가 서비스가 호스트하는 행위자에 대한 메타데이터를 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-140">The actor service allows a client to enumerate metadata about the actors that the service is hosting.</span></span> <span data-ttu-id="b8a9b-141">행위자 서비스는 분할된 상태 저장 서비스이므로 열거는 파티션에 따라 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-141">Because the actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="b8a9b-142">각 파티션에는 많은 행위자가 포함될 수 있으므로 이 열거는 일련의 페이징된 결과로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-142">Because each partition might contain many actors, the enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="b8a9b-143">페이지는 모든 페이지를 읽을 때까지 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-143">The pages are looped over until all pages are read.</span></span> <span data-ttu-id="b8a9b-144">다음 예제에서는 행위자 서비스의 한 파티션에 있는 모든 활성 행위자의 목록을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-144">The following example shows how to create a list of all active actors in one partition of an actor service:</span></span>

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

#### <a name="deleting-actors"></a><span data-ttu-id="b8a9b-145">행위자 삭제</span><span class="sxs-lookup"><span data-stu-id="b8a9b-145">Deleting actors</span></span>
<span data-ttu-id="b8a9b-146">행위자 서비스에서도 행위자를 삭제하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-146">The actor service also provides a function for deleting actors:</span></span>

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

<span data-ttu-id="b8a9b-147">행위자와 해당 상태를 삭제하는 데에 대한 자세한 내용은 [행위자 수명 주기 설명서](service-fabric-reliable-actors-lifecycle.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-147">For more information on deleting actors and their state, see the [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="b8a9b-148">사용자 지정 행위자 서비스</span><span class="sxs-lookup"><span data-stu-id="b8a9b-148">Custom actor service</span></span>
<span data-ttu-id="b8a9b-149">행위자 등록 람다를 사용하여 `ActorService`(C#) 및 `FabricActorService`(Java)에서 파생된 사용자 지정 행위자 서비스를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-149">By using the actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="b8a9b-150">이 사용자 지정 행위자 서비스에서 `ActorService`(C#) 또는 `FabricActorService`(Java)를 상속하는 서비스 클래스를 작성하여 고유한 서비스 수준 기능을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="b8a9b-151">사용자 지정 행위자 서비스는 `ActorService`(C#) 또는 `FabricActorService`(Java)로부터 행위자 런타임 기능을 모두 상속하고 고유한 서비스 메서드를 구현하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-151">A custom actor service inherits all the actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used to implement your own service methods.</span></span>

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

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="b8a9b-152">행위자 백업 및 복원 구현</span><span class="sxs-lookup"><span data-stu-id="b8a9b-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="b8a9b-153">다음 예제에서는 사용자 지정 행위자 서비스가 `ActorService`에 이미 나타난 원격 수신기를 활용하여 행위자 데이터를 백업하는 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-153">In the following example, the custom actor service exposes a method to back up actor data by taking advantage of the remoting listener already present in `ActorService`:</span></span>

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
           // store the contents of backupInfo.Directory
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
           // store the contents of backupInfo.Directory
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


<span data-ttu-id="b8a9b-154">이 예제에서 `IMyActorService`은 `IService`(C#) 또는 `Service`(Java)를 구현하는 원격 계약이고 `MyActorService`에서 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="b8a9b-155">이 원격 서비스 계약을 추가하면 `IMyActorService`의 메서드도 `ActorServiceProxy`를 통해 원격 프록시를 만들어 클라이언트에 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-155">By adding this remoting contract, methods on `IMyActorService` are now also available to a client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

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

## <a name="application-model"></a><span data-ttu-id="b8a9b-156">응용 프로그램 모델</span><span class="sxs-lookup"><span data-stu-id="b8a9b-156">Application model</span></span>
<span data-ttu-id="b8a9b-157">행위자 서비스는 Reliable Services에 속하므로 응용 프로그램 모델이 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-157">Actor services are Reliable Services, so the application model is the same.</span></span> <span data-ttu-id="b8a9b-158">그러나 행위자 프레임워크 빌드 도구는 일부 응용 프로그램 모델 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-158">However, the actor framework build tools generate some of the application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="b8a9b-159">서비스 매니페스트</span><span class="sxs-lookup"><span data-stu-id="b8a9b-159">Service manifest</span></span>
<span data-ttu-id="b8a9b-160">행위자 프레임워크 빌드 도구에서 행위자 서비스의 ServiceManifest.xml 파일의 콘텐츠를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-160">The actor framework build tools automatically generate the contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="b8a9b-161">이 파일에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-161">This file includes:</span></span>

* <span data-ttu-id="b8a9b-162">행위자 서비스 유형.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-162">Actor service type.</span></span> <span data-ttu-id="b8a9b-163">유형 이름은 행위자 프로젝트 이름에 따라 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-163">The type name is generated based on your actor's project name.</span></span> <span data-ttu-id="b8a9b-164">행위자의 지속성 특성에 따라 HasPersistedState 플래그도 적절하게 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-164">Based on the persistence attribute on your actor, the HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="b8a9b-165">코드 패키지.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-165">Code package.</span></span>
* <span data-ttu-id="b8a9b-166">구성 패키지.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-166">Config package.</span></span>
* <span data-ttu-id="b8a9b-167">장치 및 끝점.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="b8a9b-168">응용 프로그램 매니페스트.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-168">Application manifest</span></span>
<span data-ttu-id="b8a9b-169">행위자 프레임워크 빌드 도구는 행위자 서비스에 대한 기본 서비스 정의를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-169">The actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="b8a9b-170">빌드 도구가 기본 서비스 속성을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-170">The build tools populate the default service properties:</span></span>

* <span data-ttu-id="b8a9b-171">복제본 세트 수는 행위자의 지속성 특성에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-171">Replica set count is determined by the persistence attribute on your actor.</span></span> <span data-ttu-id="b8a9b-172">행위자의 지속성 특성이 변경될 때마다 기본 서비스 정의에 있는 복제본 세트 수는 적절하게 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-172">Each time the persistence attribute on your actor is changed, the replica set count in the default service definition is reset accordingly.</span></span>
* <span data-ttu-id="b8a9b-173">파티션 구성표와 범위는 전체 Int64 키 범위인 균일한 Int64로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-173">Partition scheme and range are set to Uniform Int64 with the full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="b8a9b-174">행위자에 대한 서비스 패브릭 파티션 개념</span><span class="sxs-lookup"><span data-stu-id="b8a9b-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="b8a9b-175">행위자 서비스는 분할된 상태 저장 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="b8a9b-176">행위자 서비스의 각 파티션은 일련의 행위자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="b8a9b-177">서비스 파티션은 서비스 패브릭에 있는 여러 노드에 자동으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="b8a9b-178">결과적으로 행위자 인스턴스가 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-178">Actor instances are distributed as a result.</span></span>

![행위자 분할 및 배포][5]

<span data-ttu-id="b8a9b-180">Reliable Services는 다른 파티션 구성표와 파티션 키 범위로 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="b8a9b-181">행위자 서비스는 전체 Int64 키 범위를 가진 Int64 파티션 구성표를 사용하여 파티션에 행위자를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-181">The actor service uses the Int64 partitioning scheme with the full Int64 key range to map actors to partitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="b8a9b-182">행위자 ID</span><span class="sxs-lookup"><span data-stu-id="b8a9b-182">Actor ID</span></span>
<span data-ttu-id="b8a9b-183">서비스에서 만들어진 각 행위자에는 그와 관련된 고유한 ID가 있고 `ActorId` 클래스에서 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-183">Each actor that's created in the service has a unique ID associated with it, represented by the `ActorId` class.</span></span> <span data-ttu-id="b8a9b-184">`ActorId`는 임의의 ID를 생성하여 서비스 파티션에 행위자를 균일하게 배포하기 위해 사용될 수 있는 불투명 ID 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across the service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="b8a9b-185">모든 `ActorId`는 Int64로 해시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-185">Every `ActorId` is hashed to an Int64.</span></span> <span data-ttu-id="b8a9b-186">그래서 행위자 서비스가 전체 Int64 키 범위가 있는 Int64 파티션 구성표를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-186">This is why the actor service must use an Int64 partitioning scheme with the full Int64 key range.</span></span> <span data-ttu-id="b8a9b-187">그러나 사용자 지정 ID 값은 GUID/UUID, 문자열 및 Int64를 비롯한 `ActorID`에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

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

<span data-ttu-id="b8a9b-188">GUID/UUID 및 문자열을 사용하는 경우 값은 Int64로 해시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-188">When you're using GUIDs/UUIDs and strings, the values are hashed to an Int64.</span></span> <span data-ttu-id="b8a9b-189">그러나 명시적으로 `ActorId`에 대한 Int64를 제공하는 경우 Int64는 해시를 추가하지 않고 파티션에 직접 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-189">However, when you're explicitly providing an Int64 to an `ActorId`, the Int64 will map directly to a partition without further hashing.</span></span> <span data-ttu-id="b8a9b-190">이 기술을 사용하여 행위자가 배치되는 파티션을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8a9b-190">You can use this technique to control which partition the actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8a9b-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8a9b-191">Next steps</span></span>
* [<span data-ttu-id="b8a9b-192">행위자 상태 관리</span><span class="sxs-lookup"><span data-stu-id="b8a9b-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="b8a9b-193">행위자 수명 주기 및 가비지 수집</span><span class="sxs-lookup"><span data-stu-id="b8a9b-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="b8a9b-194">행위자 API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="b8a9b-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="b8a9b-195">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="b8a9b-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="b8a9b-196">Java 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="b8a9b-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
