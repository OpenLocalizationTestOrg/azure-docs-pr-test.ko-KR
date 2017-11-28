---
title: "Azure 서비스 패브릭에서 서비스에 대 한 보안 통신 aaaHelp | Microsoft Docs"
description: "어떻게 toohelp를 보호 하는 신뢰할 수 있는 서비스에 대 한 통신의 개요는 Azure 서비스 패브릭 클러스터에서 실행 됩니다."
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
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="7176e-103">Azure 서비스 패브릭에서 서비스에 대한 통신 보호 도움말</span><span class="sxs-lookup"><span data-stu-id="7176e-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7176e-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="7176e-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="7176e-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="7176e-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="7176e-106">보안 통신의 hello 가장 중요 한 측면 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-106">Security is one of hello most important aspects of communication.</span></span> <span data-ttu-id="7176e-107">hello 신뢰할 수 있는 서비스 응용 프로그램 프레임 워크는 몇 가지 미리 작성 된 통신 스택과 tooimprove 보안을 사용할 수 있는 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-107">hello Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use tooimprove security.</span></span> <span data-ttu-id="7176e-108">이 문서 tooimprove 보안을 사용 하는 경우 원격 서비스와 Windows Communication Foundation (WCF) 통신 스택을 hello 방법에 대해 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-108">This article talks about how tooimprove security when you're using service remoting and hello Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="7176e-109">서비스 원격 기능을 사용하는 경우 서비스 보호 도움말</span><span class="sxs-lookup"><span data-stu-id="7176e-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="7176e-110">사용 하 여 기존 [예제](service-fabric-reliable-services-communication-remoting.md) 설명 하는 방법을 tooset 신뢰할 수 있는 서비스에 대 한 원격을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="7176e-111">toohelp 원격 서비스를 사용 하는 경우 서비스에 보안 설정, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-111">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="7176e-112">인터페이스를 만들 `IHelloWorldStateful`, 서비스에 대 한 원격 프로시저 호출에서 사용할 수 있는 hello 메서드를 정의 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-112">Create an interface, `IHelloWorldStateful`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="7176e-113">서비스 ´ ֲ `FabricTransportServiceRemotingListener`, hello에는 선언 `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="7176e-114">이것은 원격 호출 기능을 제공하는 `ICommunicationListener` 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="7176e-115">수신기 설정 및 보안 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="7176e-116">해당 hello 사용할 인증서를 toouse toohelp 보안 서비스 통신이 hello 클러스터의 모든 hello 노드에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-116">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="7176e-117">두 가지 방법으로 수신기 설정 및 보안 자격 증명을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="7176e-118">Hello 서비스 코드에서 직접 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-118">Provide them directly in hello service code:</span></span>

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
   2. <span data-ttu-id="7176e-119">[config 패키지](service-fabric-application-model.md)를 사용하여 제공:</span><span class="sxs-lookup"><span data-stu-id="7176e-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="7176e-120">추가 `TransportSettings` hello settings.xml 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-120">Add a `TransportSettings` section in hello settings.xml file.</span></span>

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

       <span data-ttu-id="7176e-121">이 경우 hello `CreateServiceReplicaListeners` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-121">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

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

        <span data-ttu-id="7176e-122">추가 하는 경우는 `TransportSettings` hello settings.xml 파일의 섹션 `FabricTransportRemotingListenerSettings ` 기본적으로이 섹션에서 모든 hello 설정의 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-122">If you add a `TransportSettings` section in hello settings.xml file , `FabricTransportRemotingListenerSettings ` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="7176e-123">이 경우 hello `CreateServiceReplicaListeners` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-123">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

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
3. <span data-ttu-id="7176e-124">Hello remoting 스택 hello를 사용 하는 대신 사용 하 여 보안된 서비스에 메서드를 호출 하는 경우 `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` 클래스 toocreate 서비스 프록시를 사용 하 여 `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-124">When you call methods on a secured service by using hello remoting stack, instead of using hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class toocreate a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="7176e-125">`SecurityCredentials`를 포함하는 `FabricTransportRemotingSettings`를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

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

    <span data-ttu-id="7176e-126">서비스의 일부로 hello 클라이언트 코드를 실행 하는 경우 로드할 수 있습니다 `FabricTransportRemotingSettings` hello settings.xml 파일에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-126">If hello client code is running as part of a service, you can load `FabricTransportRemotingSettings` from hello settings.xml file.</span></span> <span data-ttu-id="7176e-127">앞에서 보았듯이 비슷한 toohello 서비스 코드를 있는 HelloWorldClientTransportSettings 섹션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-127">Create a HelloWorldClientTransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="7176e-128">Hello toohello 클라이언트 코드 변경 내용을 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-128">Make hello following changes toohello client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="7176e-129">Hello에 client_name.settings.xml 파일을 만들 수 hello 클라이언트는 서비스의 일부분으로를 실행 하지 않는 경우 hello client_name.exe가 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-129">If hello client is not running as part of a service, you can create a client_name.settings.xml file in hello same location where hello client_name.exe is.</span></span> <span data-ttu-id="7176e-130">그런 다음 해당 파일에서 TransportSettings 섹션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="7176e-131">비슷한 toohello 서비스를 추가 하는 경우는 `TransportSettings` 클라이언트 settings.xml/client_name.settings.xml 섹션인 `FabricTransportRemotingSettings` 기본적으로이 섹션에서 모든 hello 설정을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-131">Similar toohello service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all hello settings from this section by default.</span></span>

    <span data-ttu-id="7176e-132">이 경우 hello 이전 코드가 더욱 간소화:</span><span class="sxs-lookup"><span data-stu-id="7176e-132">In that case, hello earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="7176e-133">WCF 기반 통신 스택을 사용하는 경우 서비스 보호 방법</span><span class="sxs-lookup"><span data-stu-id="7176e-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="7176e-134">사용 하 여 기존 [예제](service-fabric-reliable-services-communication-wcf.md) tooset WCF 기반 통신을 신뢰할 수 있는 서비스에 대 한 스택 하는 방법에 대해 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how tooset up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="7176e-135">toohelp은 WCF 기반 통신 스택을 사용 하는 경우 서비스에 보안 설정, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-135">toohelp secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="7176e-136">Toohelp 보안 hello WCF 통신 수신기 hello 서비스에 대 한 필요한 (`WcfCommunicationListener`)를 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-136">For hello service, you need toohelp secure hello WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="7176e-137">toodo이 hello 수정 `CreateServiceReplicaListeners` 메서드.</span><span class="sxs-lookup"><span data-stu-id="7176e-137">toodo this, modify hello `CreateServiceReplicaListeners` method.</span></span>

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

        // Add certificate details in hello ServiceHost credentials.
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
2. <span data-ttu-id="7176e-138">Hello 클라이언트에서 hello `WcfCommunicationClient` 클래스에서에서 만든 hello 이전 [예제](service-fabric-reliable-services-communication-wcf.md) 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-138">In hello client, hello `WcfCommunicationClient` class that was created in hello previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="7176e-139">하지만 toooverride hello 필요 `CreateClientAsync` 방식의 `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="7176e-139">But you need toooverride hello `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

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
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
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

    <span data-ttu-id="7176e-140">사용 하 여 `SecureWcfCommunicationClientFactory` toocreate WCF 통신 클라이언트 (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="7176e-140">Use `SecureWcfCommunicationClientFactory` toocreate a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="7176e-141">Hello 클라이언트 tooinvoke 서비스 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7176e-141">Use hello client tooinvoke service methods.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7176e-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7176e-142">Next steps</span></span>
* [<span data-ttu-id="7176e-143">Reliable Services에서 OWIN을 사용하는 Web API</span><span class="sxs-lookup"><span data-stu-id="7176e-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
