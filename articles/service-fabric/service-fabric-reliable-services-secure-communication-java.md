---
title: "Azure Service Fabric에서 서비스에 대한 통신 보호 도움말 | Microsoft Docs"
description: "Azure 서비스 패브릭 클러스터에서 실행되는 Reliable Services에 대한 통신을 보호하는 방법을 간략하게 설명합니다."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: c4634e3d8efb1745fffcfe3e647e43d867038716
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="b4099-103">Azure 서비스 패브릭에서 서비스에 대한 통신 보호 도움말</span><span class="sxs-lookup"><span data-stu-id="b4099-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4099-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="b4099-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="b4099-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="b4099-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="b4099-106">서비스 원격 기능을 사용하는 경우 서비스 보호 도움말</span><span class="sxs-lookup"><span data-stu-id="b4099-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="b4099-107">Reliable Services에 대한 원격 기능을 설정하는 방법에 대해 설명하는 기존 [예제](service-fabric-reliable-services-communication-remoting-java.md) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="b4099-108">서비스 원격 기능을 사용하는 경우 서비스를 보호하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="b4099-108">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="b4099-109">서비스의 원격 프로시저 호출에 사용할 수 있는 메서드를 정의하는 인터페이스 `HelloWorldStateless`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-109">Create an interface, `HelloWorldStateless`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="b4099-110">서비스는 `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` 패키지에 선언되는 `FabricTransportServiceRemotingListener`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="b4099-111">이것은 원격 호출 기능을 제공하는 `CommunicationListener` 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="b4099-112">수신기 설정 및 보안 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="b4099-113">서비스 통신을 보호하는 데 사용할 인증서는 클러스터의 모든 노드에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-113">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="b4099-114">두 가지 방법으로 수신기 설정 및 보안 자격 증명을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="b4099-115">[config 패키지](service-fabric-application-model.md)를 사용하여 제공:</span><span class="sxs-lookup"><span data-stu-id="b4099-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="b4099-116">settings.xml 파일에 `TransportSettings` 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-116">Add a `TransportSettings` section in the settings.xml file.</span></span>

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       <span data-ttu-id="b4099-117">이 경우 `createServiceInstanceListeners` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-117">In this case, the `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="b4099-118">settings.xml 파일에 접두사 없이 `TransportSettings` 섹션을 추가하면 `FabricTransportListenerSettings`은(는) 기본적으로 이 섹션의 모든 설정을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-118">If you add a `TransportSettings` section in the settings.xml file without any prefix, `FabricTransportListenerSettings` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="b4099-119">이 경우 `CreateServiceInstanceListeners` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-119">In this case, the `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="b4099-120">`microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` 클래스를 사용하여 서비스 프록시를 만드는 대신 원격 스택을 사용하여 보안 서비스에서 메서드를 호출하는 경우 `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-120">When you call methods on a secured service by using the remoting stack, instead of using the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class to create a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="b4099-121">클라이언트 코드를 서비스의 일부로 실행하는 경우 settings.xml 파일에서 `FabricTransportSettings` 를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-121">If the client code is running as part of a service, you can load `FabricTransportSettings` from the settings.xml file.</span></span> <span data-ttu-id="b4099-122">위에 나와 있는 서비스 코드와 비슷한 TransportSettings 섹션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-122">Create a TransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="b4099-123">클라이언트 코드를 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b4099-123">Make the following changes to the client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
