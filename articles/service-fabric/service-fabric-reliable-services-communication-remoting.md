---
title: "<span data-ttu-id=\"a4398-101\">Service Fabric의 서비스 원격 호출 | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"a4398-101\">Service remoting in Service Fabric | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"a4398-102\">서비스 패브릭 원격 호출을 사용하면 클라이언트와 서비스가 원격 프로시저 호출을 사용하여 서비스와 통신할 수 있도록 합니다.</span><span class=\"sxs-lookup\"><span data-stu-id=\"a4398-102\">Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.</span></span>"
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
ms.openlocfilehash: 92a8894f24c234fbf38eda086531b524cceccfc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="a4398-103">Reliable Services로 서비스 원격 호출</span><span class="sxs-lookup"><span data-stu-id="a4398-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="a4398-104">특정한 통신 프로토콜 또는 스택에 얽매여 있지 않는 서비스(예: WebAPI, WCF(Windows Communication Foundation) 등)의 경우, Reliable Services 프레임워크가 원격 메커니즘을 제공하여 서비스에 대한 원격 프로시저 호출을 신속하고 간편하게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-104">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="a4398-105">서비스에 원격 호출 설정</span><span class="sxs-lookup"><span data-stu-id="a4398-105">Set up remoting on a service</span></span>
<span data-ttu-id="a4398-106">서비스에 대한 원격 호출은 간단한 두 가지 단계로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="a4398-107">서비스로 구현할 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-107">Create an interface for your service to implement.</span></span> <span data-ttu-id="a4398-108">이 인터페이스는 서비스의 원격 프로시저 호출에 사용할 수 있는 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-108">This interface defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="a4398-109">메서드는 작업을 반환하는 비동기 메서드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-109">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="a4398-110">인터페이스는 서비스에 원격 호출 인터페이스가 있다는 것을 신호하기 위해 `Microsoft.ServiceFabric.Services.Remoting.IService` 를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-110">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="a4398-111">서비스에서 원격 수신기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="a4398-112">이것은 원격 호출 기능을 제공하는 `ICommunicationListener` 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="a4398-113">`Microsoft.ServiceFabric.Services.Remoting.Runtime` 네임스페이스는 기본 원격 전송 프로토콜을 사용하여 원격 수신기를 만드는 데 사용할 수 있는 상태 비저장 및 상태 저장 서비스에 대해 확장 메서드인 `CreateServiceRemotingListener`를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-113">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="a4398-114">참고: `Remoting` 네임스페이스는 `Microsoft.ServiceFabric.Services.Remoting`이라는 별도의 NuGet 패키지로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-114">Note: The `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="a4398-115">예를 들어 다음의 상태 비저장 서비스는 단일 메서드를 노출하여 원격 프로시저 호출에 "Hello World"를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-115">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="a4398-116">서비스 인터페이스의 인수 및 반환 형식은 간단한 형식, 복합 형식 또는 사용자 지정 형식이 가능하지만 .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx)에 의한 직렬화가 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-116">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="a4398-117">원격 서비스 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="a4398-117">Call remote service methods</span></span>
<span data-ttu-id="a4398-118">원격 스택을 사용하여 서비스에서 메서드를 호출하는 작업은 `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` 클래스를 통해 서비스에 대한 로컬 프록시를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-118">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="a4398-119">`ServiceProxy` 메서드는 서비스가 구현하는 것과 동일한 인터페이스를 사용하여 로컬 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-119">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="a4398-120">이 프록시를 통해 원격으로 인터페이스의 메서드를 간단하게 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-120">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="a4398-121">원격 호출 프레임워크는 서비스에 throw된 예외를 클라이언트에 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-121">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="a4398-122">따라서 `ServiceProxy` 을 사용하여 클라이언트에서 논리를 예외 처리하는 작업은 서비스가 throw하는 예외를 직접 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-122">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="a4398-123">서비스 프록시 수명</span><span class="sxs-lookup"><span data-stu-id="a4398-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="a4398-124">ServiceProxy 만들기는 가벼운 작업이므로 사용자가 원하는 만큼 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="a4398-125">서비스 프록시는 사용자가 필요할 때까지 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="a4398-126">사용자는 예외 발생 시 동일한 프록시를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-126">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="a4398-127">각 서비스 프록시는 유선으로 메시지를 보내는 데 사용되는 통신 클라이언트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-127">Each ServiceProxy contains communciation client used to send messages over the wire.</span></span> <span data-ttu-id="a4398-128">API를 호출하는 동안 사용된 통신 클라이언트가 유효한지 내부적으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-128">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="a4398-129">그 결과에 따라 통신 클라이언트를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-129">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="a4398-130">따라서 사용자는 예외 발생 시 serviceproxy를 다시 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-130">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="a4398-131">ServiceProxyFactory 수명</span><span class="sxs-lookup"><span data-stu-id="a4398-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="a4398-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory)는 다른 원격 인터페이스를 위한 프록시를 만드는 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="a4398-133">프록시를 만드는 데 API ServiceProxy.Create를 사용하면 프레임워크는 singelton ServiceProxyFactory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-133">If you use API ServiceProxy.Create for creating proxy, then framework creates the singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="a4398-134">[IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) 속성을 재정의해야 하는 경우 수동으로 만드는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-134">It is useful to create one manually when you need to override [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="a4398-135">팩터리는 비용이 많이 드는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-135">Factory is an expensive operation.</span></span> <span data-ttu-id="a4398-136">ServiceProxyFactory는 통신 클라이언트의 캐시를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="a4398-137">ServiceProxyFactory를 가능한 한 오랫동안 캐시하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-137">Best practice is to cache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="a4398-138">원격 예외 처리</span><span class="sxs-lookup"><span data-stu-id="a4398-138">Remoting Exception Handling</span></span>
<span data-ttu-id="a4398-139">서비스 API에 의해 throw되는 모든 원격 예외는 AggregateException으로 클라이언트에 다시 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-139">All the remote exception thrown by service API, are sent back to the client as AggregateException.</span></span> <span data-ttu-id="a4398-140">RemoteExceptions는 DataContract 직결화가 가능해야 합니다. 그렇지 않으면[ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception)이 직렬화 오류가 있는 프록시 API에 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown to the proxy API with the serialization error in it.</span></span>

<span data-ttu-id="a4398-141">ServiceProxy는 만들어진 서비스 파티션에 대한 모든 장애 조치(failover) 예외를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="a4398-142">장애 조치(Failover) 예외(영구적인 예외)가 있는 경우 끝점을 다시 확인하고 올바른 끝점으로 호출을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="a4398-143">장애 조치(Failover) 예외에 대한 재시도 횟수는 무한합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="a4398-144">TransientExceptions의 경우에는 호출만 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="a4398-145">기본 재시도 매개 변수는 [OperationRetrySettings]에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="a4398-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) 사용자는 OperationRetrySettings 개체를 ServiceProxyFactory 생성자에 전달하여 이러한 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4398-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4398-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4398-147">Next steps</span></span>
* [<span data-ttu-id="a4398-148">Reliable Services에서 OWIN을 사용하는 Web API</span><span class="sxs-lookup"><span data-stu-id="a4398-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="a4398-149">Reliable Services와 WCF 통신</span><span class="sxs-lookup"><span data-stu-id="a4398-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="a4398-150">Reliable Services에 대한 통신 보안 유지</span><span class="sxs-lookup"><span data-stu-id="a4398-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
