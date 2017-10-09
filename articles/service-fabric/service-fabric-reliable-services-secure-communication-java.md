---
title: "Azure 서비스 패브릭에서 서비스에 대 한 보안 통신 aaaHelp | Microsoft Docs"
description: "어떻게 toohelp를 보호 하는 신뢰할 수 있는 서비스에 대 한 통신의 개요는 Azure 서비스 패브릭 클러스터에서 실행 됩니다."
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
ms.openlocfilehash: 14db54d50c35478c1f2c156de0dba36f1427c8cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="3ef62-103">Azure 서비스 패브릭에서 서비스에 대한 통신 보호 도움말</span><span class="sxs-lookup"><span data-stu-id="3ef62-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ef62-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="3ef62-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="3ef62-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="3ef62-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="3ef62-106">서비스 원격 기능을 사용하는 경우 서비스 보호 도움말</span><span class="sxs-lookup"><span data-stu-id="3ef62-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="3ef62-107">사용할 기존 [예제](service-fabric-reliable-services-communication-remoting-java.md) 설명 하는 방법을 tooset 신뢰할 수 있는 서비스에 대 한 원격을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="3ef62-108">toohelp 원격 서비스를 사용 하는 경우 서비스에 보안 설정, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-108">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="3ef62-109">인터페이스를 만들 `HelloWorldStateless`, 서비스에 대 한 원격 프로시저 호출에서 사용할 수 있는 hello 메서드를 정의 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-109">Create an interface, `HelloWorldStateless`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="3ef62-110">서비스 ´ ֲ `FabricTransportServiceRemotingListener`, hello에는 선언 `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="3ef62-111">이것은 원격 호출 기능을 제공하는 `CommunicationListener` 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="3ef62-112">수신기 설정 및 보안 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="3ef62-113">해당 hello 사용할 인증서를 toouse toohelp 보안 서비스 통신이 hello 클러스터의 모든 hello 노드에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-113">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="3ef62-114">두 가지 방법으로 수신기 설정 및 보안 자격 증명을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="3ef62-115">[config 패키지](service-fabric-application-model.md)를 사용하여 제공:</span><span class="sxs-lookup"><span data-stu-id="3ef62-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="3ef62-116">추가 `TransportSettings` hello settings.xml 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-116">Add a `TransportSettings` section in hello settings.xml file.</span></span>

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

       <span data-ttu-id="3ef62-117">이 경우 hello `createServiceInstanceListeners` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-117">In this case, hello `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="3ef62-118">추가 하는 경우는 `TransportSettings` 모든 접두사 없이 hello settings.xml 파일에 섹션 `FabricTransportListenerSettings` 기본적으로이 섹션에서 모든 hello 설정의 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-118">If you add a `TransportSettings` section in hello settings.xml file without any prefix, `FabricTransportListenerSettings` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="3ef62-119">이 경우 hello `CreateServiceInstanceListeners` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-119">In this case, hello `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="3ef62-120">Hello remoting 스택 hello를 사용 하는 대신 사용 하 여 보안된 서비스에 메서드를 호출 하는 경우 `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` 클래스 toocreate 서비스 프록시를 사용 하 여 `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-120">When you call methods on a secured service by using hello remoting stack, instead of using hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class toocreate a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="3ef62-121">서비스의 일부로 hello 클라이언트 코드를 실행 하는 경우 로드할 수 있습니다 `FabricTransportSettings` hello settings.xml 파일에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-121">If hello client code is running as part of a service, you can load `FabricTransportSettings` from hello settings.xml file.</span></span> <span data-ttu-id="3ef62-122">앞에서 보았듯이 비슷한 toohello 서비스 코드를 있는 TransportSettings 섹션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-122">Create a TransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="3ef62-123">Hello toohello 클라이언트 코드 변경 내용을 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef62-123">Make hello following changes toohello client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
