---
title: "Reliable Services WCF 통신 스택 | Microsoft Docs"
description: "서비스 패브릭의 기본 제공 WCF 통신 스택은 Reliable Services를 위한 클라이언트-서비스 WCF 통신을 제공합니다."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/07/2017
ms.author: bharatn
ms.openlocfilehash: 7037620ebdc26a9f18531064bf45d058f5060e39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="784c3-103">Reliable Services에 대한 WCF 기반 통신 스택</span><span class="sxs-lookup"><span data-stu-id="784c3-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="784c3-104">Reliable Services 프레임워크를 사용하면 서비스 작성자가 서비스에 사용하려는 통신 스택을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="784c3-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span></span> <span data-ttu-id="784c3-105">선택한 통신 스택을 **CreateServiceReplicaListeners 또는 CreateServiceInstanceListeners** 메서드에서 반환되는 [ICommunicationListener](service-fabric-reliable-services-communication.md) 를 통해 플러그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="784c3-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="784c3-106">이 프레임워크는 WCF 기반 통신을 사용하려는 서비스 작성자를 위한 WCF(Windows Communication Foundation) 기반 통신 스택 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="784c3-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="784c3-107">WCF 통신 수신기</span><span class="sxs-lookup"><span data-stu-id="784c3-107">WCF Communication Listener</span></span>
<span data-ttu-id="784c3-108">**ICommunicationListener**의 WCF 관련 구현은 **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** 클래스에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="784c3-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="784c3-109">서비스 계약의 형식이 있다고 가정합니다 `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="784c3-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="784c3-110">다음과 같은 방식으로 서비스에서 WCF 통신 수신기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="784c3-110">We can create a WCF communication listener in the service the following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // The name of the endpoint configured in the ServiceManifest under the Endpoints section
            // that identifies the endpoint that the WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate the binding information that you want the service to use.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-the-wcf-communication-stack"></a><span data-ttu-id="784c3-111">WCF 통신 스택에 대한 클라이언트 작성</span><span class="sxs-lookup"><span data-stu-id="784c3-111">Writing clients for the WCF communication stack</span></span>
<span data-ttu-id="784c3-112">WCF를 사용하여 서비스와 통신하는 클라이언트를 작성하는 경우 이 프레임워크에서는 **ClientCommunicationFactoryBase**의 WCF 특정 구현인 [WcfClientCommunicationFactory](service-fabric-reliable-services-communication.md)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="784c3-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="784c3-113">WCF 통신 채널은 **WcfCommunicationClientFactory**에서 만든 **WcfCommunicationClient**에서 액세스될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="784c3-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="784c3-114">클라이언트 코드는 **ServicePartitionClient**를 구현하는 **WcfCommunicationClient**와 함께 **WcfCommunicationClientFactory**를 사용하여 서비스 끝점을 결정하고 서비스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="784c3-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with the ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call the service to perform the operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="784c3-115">기본 ServicePartitionResolver는 클라이언트가 서비스와 동일한 클러스터에서 실행되고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="784c3-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span></span> <span data-ttu-id="784c3-116">그렇지 않은 경우 ServicePartitionResolver 개체를 만들고 클러스터 연결 끝점에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="784c3-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="784c3-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="784c3-117">Next steps</span></span>
* [<span data-ttu-id="784c3-118">Reliable Services 원격을 사용하여 원격 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="784c3-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="784c3-119">Reliable Services에서 OWIN을 사용하는 Web API</span><span class="sxs-lookup"><span data-stu-id="784c3-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="784c3-120">Reliable Services에 대한 통신 보안 유지</span><span class="sxs-lookup"><span data-stu-id="784c3-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

