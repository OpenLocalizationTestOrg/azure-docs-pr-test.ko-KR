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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Azure 서비스 패브릭에서 서비스에 대한 통신 보호 도움말
> [!div class="op_single_selector"]
> * [Windows에서 C#](service-fabric-reliable-services-secure-communication.md)
> * [Linux에서 Java](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>서비스 원격 기능을 사용하는 경우 서비스 보호 도움말
사용할 기존 [예제](service-fabric-reliable-services-communication-remoting-java.md) 설명 하는 방법을 tooset 신뢰할 수 있는 서비스에 대 한 원격을 합니다. toohelp 원격 서비스를 사용 하는 경우 서비스에 보안 설정, 다음이 단계를 수행 합니다.

1. 인터페이스를 만들 `HelloWorldStateless`, 서비스에 대 한 원격 프로시저 호출에서 사용할 수 있는 hello 메서드를 정의 하는 합니다. 서비스 ´ ֲ `FabricTransportServiceRemotingListener`, hello에는 선언 `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` 패키지 합니다. 이것은 원격 호출 기능을 제공하는 `CommunicationListener` 구현입니다.

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
2. 수신기 설정 및 보안 자격 증명을 추가합니다.

    해당 hello 사용할 인증서를 toouse toohelp 보안 서비스 통신이 hello 클러스터의 모든 hello 노드에 설치 되어 있는지 확인 합니다. 두 가지 방법으로 수신기 설정 및 보안 자격 증명을 제공할 수 있습니다.

   1. [config 패키지](service-fabric-application-model.md)를 사용하여 제공:

       추가 `TransportSettings` hello settings.xml 파일의 섹션입니다.

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

       이 경우 hello `createServiceInstanceListeners` 메서드는 다음과 같습니다.

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        추가 하는 경우는 `TransportSettings` 모든 접두사 없이 hello settings.xml 파일에 섹션 `FabricTransportListenerSettings` 기본적으로이 섹션에서 모든 hello 설정의 로드 합니다.

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        이 경우 hello `CreateServiceInstanceListeners` 메서드는 다음과 같습니다.

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. Hello remoting 스택 hello를 사용 하는 대신 사용 하 여 보안된 서비스에 메서드를 호출 하는 경우 `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` 클래스 toocreate 서비스 프록시를 사용 하 여 `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`합니다.

    서비스의 일부로 hello 클라이언트 코드를 실행 하는 경우 로드할 수 있습니다 `FabricTransportSettings` hello settings.xml 파일에서 합니다. 앞에서 보았듯이 비슷한 toohello 서비스 코드를 있는 TransportSettings 섹션을 만듭니다. Hello toohello 클라이언트 코드 변경 내용을 다음을 확인 합니다.

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
