---
title: "aaaReliable 서비스 WCF 통신 스택을 | Microsoft Docs"
description: "서비스 패브릭에서 hello 기본 제공 WCF 통신 스택을 신뢰할 수 있는 서비스에 대 한 클라이언트-서비스 WCF 통신을 제공합니다."
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
ms.openlocfilehash: 7feebef4d46a6ae66d05129f47f9b5911e82aec9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a>Reliable Services에 대한 WCF 기반 통신 스택
hello 신뢰할 수 있는 서비스 프레임 워크에서는 서비스 작성자 toochoose hello 통신 스택을 서비스에 대 한 toouse 싶어한다는 합니다. Hello 통해 자신이 선택한 hello 통신 스택을에 연결할 수 **ICommunicationListener** hello에서 반환 된 [CreateServiceReplicaListeners 또는 CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) 메서드. hello framework toouse WCF 기반 통신 하려는 서비스 작성자를 위한 Windows Communication Foundation (WCF) hello에 따라 hello 통신 스택 구현을 제공 합니다.

## <a name="wcf-communication-listener"></a>WCF 통신 수신기
hello WCF 관련 구현 **ICommunicationListener** hello 제공한 **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** 클래스입니다.

서비스 계약의 형식이 있다고 가정합니다 `ICalculator`

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

Hello 서비스 hello 방식으로 다음에서 WCF 통신 수신기를 만들 수 했습니다.

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // hello name of hello endpoint configured in hello ServiceManifest under hello Endpoints section
            // that identifies hello endpoint that hello WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate hello binding information that you want hello service toouse.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-hello-wcf-communication-stack"></a>WCF 통신 스택 hello에 대 한 클라이언트를 작성합니다.
WCF, hello 프레임 워크를 사용 하 여 서비스와 toocommunicate 제공 하는 클라이언트를 작성 하기 위한 **WcfClientCommunicationFactory**의 WCF 관련 hello 구현인 [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

WCF 통신 채널을 hello hello에서 액세스할 수 **WcfCommunicationClient** hello에서 만든 **WcfCommunicationClientFactory**합니다.

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

클라이언트 코드는 hello를 사용할 수 있는 **WcfCommunicationClientFactory** hello 함께 **WcfCommunicationClient** 구현 하는 **ServicePartitionClient** toodetermine 서비스 끝점을 hello 및 hello 서비스와 통신 합니다.

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with hello ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call hello service tooperform hello operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> hello 기본 ServicePartitionResolver hello 클라이언트 hello 서비스와 동일한 클러스터에서 실행 중인 가정 합니다. 않은 경우 하지 hello, ServicePartitionResolver 개체를 만들고 hello 클러스터 연결 끝점에 전달 합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* [Reliable Services 원격을 사용하여 원격 프로시저 호출](service-fabric-reliable-services-communication-remoting.md)
* [Reliable Services에서 OWIN을 사용하는 Web API](service-fabric-reliable-services-communication-webapi.md)
* [Reliable Services에 대한 통신 보안 유지](service-fabric-reliable-services-secure-communication.md)

