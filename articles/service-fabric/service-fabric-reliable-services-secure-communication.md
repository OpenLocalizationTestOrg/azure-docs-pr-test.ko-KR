---
title: "Azure Service Fabric에서 서비스에 대한 통신 보호 도움말 | Microsoft Docs"
description: "Azure 서비스 패브릭 클러스터에서 실행되는 Reliable Services에 대한 통신을 보호하는 방법을 간략하게 설명합니다."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 53119244f8f09c0c6c43f43761af1cc074f8d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="f042d-103">Azure 서비스 패브릭에서 서비스에 대한 통신 보호 도움말</span><span class="sxs-lookup"><span data-stu-id="f042d-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f042d-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="f042d-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="f042d-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="f042d-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="f042d-106">통신의 가장 중요한 측면 중 하나는 보안입니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-106">Security is one of the most important aspects of communication.</span></span> <span data-ttu-id="f042d-107">Reliable Services 응용 프로그램 프레임워크는 보안을 향상시키는 데 사용할 수 있는 미리 빌드된 통신 스택 및 도구 몇 가지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-107">The Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use to improve security.</span></span> <span data-ttu-id="f042d-108">이 문서에서는 서비스 원격 기능 및 WCF(Windows Communication Foundation) 통신 스택을 사용하는 경우 보안을 개선하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-108">This article talks about how to improve security when you're using service remoting and the Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="f042d-109">서비스 원격 기능을 사용하는 경우 서비스 보호 도움말</span><span class="sxs-lookup"><span data-stu-id="f042d-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="f042d-110">Reliable Services에 대한 원격 기능을 설정하는 방법에 대해 설명하는 기존 [예제](service-fabric-reliable-services-communication-remoting.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="f042d-111">서비스 원격 기능을 사용하는 경우 서비스를 보호하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f042d-111">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="f042d-112">서비스의 원격 프로시저 호출에 사용할 수 있는 메서드를 정의하는 인터페이스 `IHelloWorldStateful`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-112">Create an interface, `IHelloWorldStateful`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="f042d-113">서비스는 `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` 네임스페이스에 선언되는 `FabricTransportServiceRemotingListener`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="f042d-114">이것은 원격 호출 기능을 제공하는 `ICommunicationListener` 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="f042d-115">수신기 설정 및 보안 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="f042d-116">서비스 통신을 보호하는 데 사용할 인증서는 클러스터의 모든 노드에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-116">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="f042d-117">두 가지 방법으로 수신기 설정 및 보안 자격 증명을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="f042d-118">서비스 코드에서 직접 제공:</span><span class="sxs-lookup"><span data-stu-id="f042d-118">Provide them directly in the service code:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. <span data-ttu-id="f042d-119">[config 패키지](service-fabric-application-model.md)를 사용하여 제공:</span><span class="sxs-lookup"><span data-stu-id="f042d-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="f042d-120">settings.xml 파일에 `TransportSettings` 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-120">Add a `TransportSettings` section in the settings.xml file.</span></span>

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       <span data-ttu-id="f042d-121">이 경우 `CreateServiceReplicaListeners` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-121">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        <span data-ttu-id="f042d-122">settings.xml 파일에 `TransportSettings` 섹션을 추가하면 `FabricTransportRemotingListenerSettings `는 기본적으로 이 섹션의 모든 설정을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-122">If you add a `TransportSettings` section in the settings.xml file , `FabricTransportRemotingListenerSettings ` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="f042d-123">이 경우 `CreateServiceReplicaListeners` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-123">In this case, the `CreateServiceReplicaListeners` method will look like this:</span></span>

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. <span data-ttu-id="f042d-124">`Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` 클래스를 사용하여 서비스 프록시를 만드는 대신 원격 스택을 사용하여 보안 서비스에서 메서드를 호출하는 경우 `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-124">When you call methods on a secured service by using the remoting stack, instead of using the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class to create a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="f042d-125">`SecurityCredentials`를 포함하는 `FabricTransportRemotingSettings`를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="f042d-126">클라이언트 코드를 서비스의 일부로 실행하는 경우 settings.xml 파일에서 `FabricTransportRemotingSettings` 를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-126">If the client code is running as part of a service, you can load `FabricTransportRemotingSettings` from the settings.xml file.</span></span> <span data-ttu-id="f042d-127">위에 나와 있는 서비스 코드와 비슷한 HelloWorldClientTransportSettings 섹션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-127">Create a HelloWorldClientTransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="f042d-128">클라이언트 코드를 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-128">Make the following changes to the client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="f042d-129">클라이언트를 서비스의 일부로 실행하지 않는 경우에는 client_name.exe와 같은 위치에 client_name.settings.xml 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-129">If the client is not running as part of a service, you can create a client_name.settings.xml file in the same location where the client_name.exe is.</span></span> <span data-ttu-id="f042d-130">그런 다음 해당 파일에서 TransportSettings 섹션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="f042d-131">서비스와 마찬가지로 클라이언트 settings.xml/client_name.settings.xml에 `TransportSettings` 섹션을 추가하면 `FabricTransportRemotingSettings`는 기본적으로 이 섹션의 모든 설정을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-131">Similar to the service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all the settings from this section by default.</span></span>

    <span data-ttu-id="f042d-132">그러면 앞의 코드를 더 간략하게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-132">In that case, the earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="f042d-133">WCF 기반 통신 스택을 사용하는 경우 서비스 보호 방법</span><span class="sxs-lookup"><span data-stu-id="f042d-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="f042d-134">Reliable Services에 대한 WCF 기반 통신 스택을 설정하는 방법을 설명하는 기존 [예제](service-fabric-reliable-services-communication-wcf.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how to set up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="f042d-135">WCF 기반 통신 스택을 사용하는 경우 서비스를 보호하려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="f042d-135">To help secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="f042d-136">서비스의 경우 만든 WCF 통신 수신기(`WcfCommunicationListener`)를 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-136">For the service, you need to help secure the WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="f042d-137">이 작업을 수행하려면 `CreateServiceReplicaListeners` 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-137">To do this, modify the `CreateServiceReplicaListeners` method.</span></span>

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in the ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. <span data-ttu-id="f042d-138">클라이언트에서는 이전 [예제](service-fabric-reliable-services-communication-wcf.md)에서 만든 `WcfCommunicationClient` 클래스가 변경되지 않고 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-138">In the client, the `WcfCommunicationClient` class that was created in the previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="f042d-139">그러나 `WcfCommunicationClientFactory`의 `CreateClientAsync` 메서드를 재정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-139">But you need to override the `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details to the ChannelFactory credentials.
            // These credentials will be used by the clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    <span data-ttu-id="f042d-140">`SecureWcfCommunicationClientFactory`를 사용하여 WCF 통신 클라이언트(`WcfCommunicationClient`)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-140">Use `SecureWcfCommunicationClientFactory` to create a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="f042d-141">클라이언트를 사용하여 서비스 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f042d-141">Use the client to invoke service methods.</span></span>

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a><span data-ttu-id="f042d-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f042d-142">Next steps</span></span>
* [<span data-ttu-id="f042d-143">Reliable Services에서 OWIN을 사용하는 Web API</span><span class="sxs-lookup"><span data-stu-id="f042d-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
