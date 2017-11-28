---
title: "서비스 패브릭에서 aaaService 원격 | Microsoft Docs"
description: "서비스 패브릭 원격 클라이언트 및 원격 프로시저 호출을 사용 하 여 서비스를 사용 하 여 toocommunicate 서비스입니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="f550f-103">Reliable Services로 서비스 원격 호출</span><span class="sxs-lookup"><span data-stu-id="f550f-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="f550f-104">Hello 신뢰할 수 있는 서비스 프레임 워크 remoting 메커니즘 tooquickly 제공 및 원격 프로시저 호출을 쉽게 설정할 tooa 특정 통신 프로토콜 또는 WebAPI, Windows Communication Foundation (WCF), 또는 다른 사용자에 게 처럼 스택에서 하지 않은 서비스를 연결에 대 한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-104">For services that are not tied tooa particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="f550f-105">서비스에 원격 호출 설정</span><span class="sxs-lookup"><span data-stu-id="f550f-105">Set up remoting on a service</span></span>
<span data-ttu-id="f550f-106">서비스에 대한 원격 호출은 간단한 두 가지 단계로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="f550f-107">서비스 tooimplement에 대 한 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-107">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="f550f-108">이 인터페이스는 서비스에 대 한 원격 프로시저 호출에서 사용할 수 있는 hello 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-108">This interface defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="f550f-109">hello 메서드는 작업 반환 해야 비동기 메서드.</span><span class="sxs-lookup"><span data-stu-id="f550f-109">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="f550f-110">hello 인터페이스를 구현 해야 `Microsoft.ServiceFabric.Services.Remoting.IService` 서비스 hello toosignal remoting 인터페이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-110">hello interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="f550f-111">서비스에서 원격 수신기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="f550f-112">이것은 원격 호출 기능을 제공하는 `ICommunicationListener` 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="f550f-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` 는 확장 메서드를 포함 하는 네임 스페이스`CreateServiceRemotingListener` 되는 상태 비저장 및 상태 저장 서비스에 대 한 사용된 toocreate remoting 수신기를 사용할 수도 hello 기본 remoting 전송 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="f550f-114">참고: hello `Remoting` 네임 스페이스 라는 별도 nuget 패키지로 제공 됩니다.`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="f550f-114">Note: hello `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="f550f-115">예를 들어 hello 다음과 같은 상태 비저장 서비스 노출 원격 프로시저 호출을 통해 단일 메서드 tooget "Hello World" 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-115">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> <span data-ttu-id="f550f-116">hello 인수와 hello 반환 hello 서비스 인터페이스의 형식에는 임의의 단순, 복합, 또는 사용자 지정 형식으로 될 수 있지만 hello.NET으로 직렬화 해야 [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-116">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable by hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="f550f-117">원격 서비스 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="f550f-117">Call remote service methods</span></span>
<span data-ttu-id="f550f-118">Hello 통해 로컬 프록시 toohello 서비스를 사용 하 여 수행 됩니다 hello remoting 스택을 사용 하 여 서비스에서 메서드를 호출 `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-118">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="f550f-119">hello `ServiceProxy` 메서드 서비스 hello 동일한 인터페이스를 구현 하는 hello를 사용 하 여 로컬 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-119">hello `ServiceProxy` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="f550f-120">해당 프록시를 호출 하면 메서드 hello 인터페이스에 원격으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-120">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="f550f-121">hello remoting 프레임 워크 hello 서비스 toohello 클라이언트에서 throw 된 예외를 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-121">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="f550f-122">따라서 예외 처리 논리를 사용 하 여 hello 클라이언트에서 `ServiceProxy` hello 서비스에서 throw 하는 예외를 직접 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-122">So exception-handling logic at hello client by using `ServiceProxy` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="f550f-123">서비스 프록시 수명</span><span class="sxs-lookup"><span data-stu-id="f550f-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="f550f-124">ServiceProxy 만들기는 가벼운 작업이므로 사용자가 원하는 만큼 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="f550f-125">서비스 프록시는 사용자가 필요할 때까지 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="f550f-126">사용자를 재사용할 수 예외 발생 시 동일한 프록시 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-126">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="f550f-127">각 ServiceProxy hello 유선으로 통신 사용 되는 클라이언트 toosend 메시지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-127">Each ServiceProxy contains communciation client used toosend messages over hello wire.</span></span> <span data-ttu-id="f550f-128">API를 호출 하는 동안 사용 되는 통신 클라이언트가 유효한 경우 내부 검사 toosee가 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-128">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="f550f-129">이 결과에 따라 다시 만듭니다 hello 통신 클라이언트를.</span><span class="sxs-lookup"><span data-stu-id="f550f-129">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="f550f-130">따라서 사용자는 toorecreate serviceproxy 예외 발생 시 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-130">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="f550f-131">ServiceProxyFactory 수명</span><span class="sxs-lookup"><span data-stu-id="f550f-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="f550f-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory)는 다른 원격 인터페이스를 위한 프록시를 만드는 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="f550f-133">프록시를 만들기 위한 ServiceProxy.Create API를 사용 하는 경우 프레임 워크는 hello singelton ServiceProxyFactory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-133">If you use API ServiceProxy.Create for creating proxy, then framework creates hello singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="f550f-134">경우에 하나의 유용한 toocreate 수동으로 toooverride 필요한 [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-134">It is useful toocreate one manually when you need toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="f550f-135">팩터리는 비용이 많이 드는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-135">Factory is an expensive operation.</span></span> <span data-ttu-id="f550f-136">ServiceProxyFactory는 통신 클라이언트의 캐시를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="f550f-137">최선의 방법은 가능한 한 오랫동안에 대 한 ServiceProxyFactory toocache입니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-137">Best practice is toocache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="f550f-138">원격 예외 처리</span><span class="sxs-lookup"><span data-stu-id="f550f-138">Remoting Exception Handling</span></span>
<span data-ttu-id="f550f-139">서비스 API에서 throw 된 모든 hello 원격 예외 AggregateException 백 toohello 클라이언트를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-139">All hello remote exception thrown by service API, are sent back toohello client as AggregateException.</span></span> <span data-ttu-id="f550f-140">RemoteExceptions 그렇지 않으면 DataContract 직렬화 가능 해야 [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) hello serialization 오류와 함께 toohello 프록시 API에 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown toohello proxy API with hello serialization error in it.</span></span>

<span data-ttu-id="f550f-141">ServiceProxy에서에 대해 만들어집니다 hello 서비스 파티션에 대 한 모든 장애 조치 예외 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="f550f-142">다시 hello 올바른 끝점으로 장애 조치 Exceptions(Non-Transient Exceptions) 및 다시 시도 hello 호출이 있는 경우 hello 끝점을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="f550f-143">장애 조치(Failover) 예외에 대한 재시도 횟수는 무한합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="f550f-144">TransientExceptions, 발생 한 경우만 다시 시도 hello 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="f550f-145">기본 재시도 매개 변수는 [OperationRetrySettings]에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="f550f-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) 사용자는 OperationRetrySettings 개체 tooServiceProxyFactory 생성자에 전달 하 여 이러한 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f550f-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f550f-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f550f-147">Next steps</span></span>
* [<span data-ttu-id="f550f-148">Reliable Services에서 OWIN을 사용하는 Web API</span><span class="sxs-lookup"><span data-stu-id="f550f-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="f550f-149">Reliable Services와 WCF 통신</span><span class="sxs-lookup"><span data-stu-id="f550f-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="f550f-150">Reliable Services에 대한 통신 보안 유지</span><span class="sxs-lookup"><span data-stu-id="f550f-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
