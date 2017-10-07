---
title: "aaaConnect Azure 서비스 패브릭 서비스와 통신 하 고 | Microsoft Docs"
description: "Tooresolve, 연결, 하 고 서비스 패브릭 서비스와 통신 하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>서비스 패브릭에서 서비스와 연결 및 통신
서비스 패브릭에서 서비스는 일반적으로 여러 VM에 배포된 서비스 패브릭 클러스터의 임의 위치에서 실행됩니다. 서비스 패브릭에서 hello 서비스 소유자에 의해 또는 자동으로 한곳 tooanother에서 이동할 수 있습니다. 서비스는 정적으로 연결 된 tooa 특정 컴퓨터나 주소 없습니다.

서비스 패브릭 응용 프로그램은 일반적으로 여러 가지 서비스로 구성되며, 각 서비스는 전문적인 작업을 수행합니다. 이러한 서비스는 웹 응용 프로그램의 다른 부분 렌더링 등의 전체 기능을 서로 tooform와 통신할 수 있습니다. Tooand 연결 하는 응용 프로그램 서비스와 통신 하는 클라이언트도 있습니다. 이 문서에서는 방법 및 서비스 패브릭에서 서비스 간에 통신을 tooset 합니다.

이 Microsoft Virtual Academy 비디오는 서비스 통신에 대해서도 설명합니다.<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>사용자 고유의 프로토콜 가져오기
서비스 패브릭 서비스의 hello 수명 주기 관리를 지원 하지만 서비스에 수행할 작업에 대 한 결정을 만들지 않습니다. 이는 통신을 포함합니다. 들어오는 요청에 대 한 끝점을 서비스의 기회 tooset 있는 서비스 패브릭 서비스를 열 때 어떤 프로토콜 또는 통신 스택을 사용 하 여 원하는 합니다. 서비스는 URI와 같은 모든 주소 지정 스키마를 사용하는 기본 **IP:포트** 주소에 대한 수신 대기 상태입니다. 여러 서비스 인스턴스 또는 복제본은 쿼리에서 toouse 다른 포트를 필요로 하거나 windows에서 hello http.sys 커널 드라이버와 같은 포트 공유 메커니즘을 사용 하는 호스트 프로세스를 공유할 수 있습니다. 두 경우 모두, 호스트 프로세스의 각 서비스 인스턴스 또는 복제본에 고유한 주소 지정이 가능해야 합니다.

![서비스 끝점][1]

## <a name="service-discovery-and-resolution"></a>서비스 검색 및 확인
분산된 시스템 서비스는 시간이 지남에 따라 tooanother 하나의 컴퓨터에서에서 이동할 수 있습니다. 이는 리소스 분산, 업그레이드, 장애 조치(failover), 확장을 포함하여 여러 가지 이유로 발생할 수 있습니다. 즉, 서비스 끝점 주소 변경 hello 서비스 toonodes 서로 다른 IP 주소로 이동 하 고 hello 서비스 동적으로 선택 된 포트를 사용 하는 경우 서로 다른 포트에서 열 수 있습니다.

![서비스 배포][7]

서비스 패브릭 검색 및 서비스 라고 하는 해결 hello 명명 서비스를 제공 합니다. hello 명명 서비스 관리 매핑하는 테이블을 명명 된 서비스 인스턴스 toohello 끝점 주소에서 수신 합니다. 서비스 패브릭의 모든 명명된 서비스 인스턴스에는 URI로 나타내는 고유한 이름(예: `"fabric:/MyApplication/MyService"`)이 있습니다. hello 서비스의 hello 이름 hello 서비스의 hello 수명 동안 변경 되지 않는 hello 끝점 주소에만 서비스를 이동 하는 경우 변경 될 수 있는 합니다. 이 유사한 toowebsites 상수 Url 않았지만 hello IP 주소가 변경 될 수 있습니다. 있으며 웹 사이트 Url tooIP 주소 확인 되 면 hello web에서 유사한 tooDNS 서비스 패브릭 서비스 이름은 tootheir 끝점 주소에 매핑하는 등록자입니다.

![서비스 끝점][2]

해결 하 고 연결 tooservices hello 루프에서 실행 하는 단계를 수행 해야 합니다.

* **해결**: 서비스에서 게시 Get hello 끝점 hello 서비스 이름을 지정 합니다.
* **연결**: toohello 서비스를 사용 하 여 해당 끝점의 프로토콜 무엇이 든를 통해 연결 합니다.
* **다시 시도**: 여러 가지 이유로 예를 들어 hello 마지막 시간 hello 끝점 주소 해결 된 이후 hello 서비스 이동한 경우에 대 한 연결 시도가 실패할 수 있습니다. 이 경우 앞에 해결 hello 및 연결 단계 필요, 다시 시도 toobe 및 hello 연결이 성공할 때까지이 주기가 반복 됩니다.

## <a name="connecting-tooother-services"></a>Tooother 서비스 연결
Tooeach 연결 된 서비스는 클러스터 내의 다른 일반적으로 직접 액세스할 수 다른 서비스의 끝점 hello hello 노드가 클러스터에서 hello에 있기 때문에 동일한 로컬 네트워크입니다. toomake 서비스 간에 더 쉽게 tooconnect 이면 서비스 패브릭 명명 서비스를 hello를 사용 하는 추가 서비스를 제공 합니다. DNS 서비스 및 역방향 프록시 서비스.


### <a name="dns-service"></a>DNS 서비스
많은 서비스, 특히 컨테이너 화 된 서비스는 기존 URL 이름이 수 있으므로 수 tooresolve 되 고 hello 표준 DNS 프로토콜 (아님 hello 서비스 이름 지정 프로토콜)를 사용 하 여이 매우 편리 하 게 응용 프로그램에서 특히 "리프트 있고, 이동" 시나리오입니다. 이것이 hello DNS 서비스입니다. Toomap DNS 이름을 tooa 서비스 명명 있으며 따라서 끝점 IP 주소를 확인 합니다. 

다음 다이어그램에서는 hello hello 서비스 패브릭 클러스터에서 실행 되는 DNS 서비스에서와 같이 hello로 다음 hello 명명 서비스 tooreturn hello 끝점 주소 tooconnect를 해결 하는 DNS 이름 tooservice 이름을 매핑합니다. hello 서비스에 대 한 DNS 이름은 hello hello 생성 시 제공 됩니다. 

![서비스 끝점][9]

에 대 한 자세한 내용은 toouse hello DNS 서비스를 확인 하려면 어떻게 [Azure 서비스 패브릭에서 DNS 서비스](service-fabric-dnsservice.md) 문서.

### <a name="reverse-proxy-service"></a>역방향 프록시 서비스
hello 역방향 프록시는 HTTPS를 포함 하 여 HTTP 끝점을 노출 하는 hello 클러스터에서 서비스를 해결 합니다. hello 역방향 프록시 크게 간소화 됩니다. 다른 서비스 호출 및 해당 메서드는 특정 함으로써 URI 형식 및 핸들 hello 해결 연결, 재시도에 필요한 단계를 사용 하 여 다른 하나의 서비스 toocommunicate hello 명명 서비스. 즉,이 URL을 호출 하기만 하 여 다른 서비스를 호출할 때 hello 명명 서비스를 숨깁니다.

![서비스 끝점][10]

Toouse hello 모드 해제 프록시 서비스를 반대로 하는 방법에 대 한 자세한 내용은 참조 [역방향 프록시 Azure 서비스 패브릭에서](service-fabric-reverseproxy.md) 문서.

## <a name="connections-from-external-clients"></a>외부 클라이언트에서 연결
Tooeach 연결 된 서비스는 클러스터 내의 다른 일반적으로 직접 액세스할 수 다른 서비스의 끝점 hello hello 노드가 클러스터에서 hello에 있기 때문에 동일한 로컬 네트워크입니다. 그러나 일부 환경에서는 클러스터가 제한된 포트 집합을 통한 외부 수신 트래픽을 경로 지정하는 부하 분산 장치 뒤에 있을 수 있습니다. 이러한 경우 서비스는 서로 통신할 및 주소를 사용 하 여 hello 명명 서비스 있지만 추가 단계 수행한 tooallow 외부 클라이언트 tooconnect tooservices 여야 합니다. 해결 여전히 수 있습니다.

## <a name="service-fabric-in-azure"></a>Azure의 서비스 패브릭
Azure의 서비스 패브릭 클러스터는 Azure 부하 분산 장치 뒤에 배치됩니다. 모든 외부 트래픽이 toohello 클러스터 hello 부하 분산 장치를 통과 해야 합니다. hello 부하 분산 장치는 자동으로 트래픽을 전달에 주어진된 포트 tooa 임의 인바운드 *노드* 있는 hello 동일한 포트를 엽니다. hello Azure 부하 분산 장치만 알고 hello에 열린 포트에 대 한 *노드*, 개별 포트 열기에 대해 알지 못하는 *서비스*합니다.

![Azure 부하 분산 장치 및 서비스 패브릭 토폴로지][3]

예를 들어 포트 순서 tooaccept 외부 트래픽을에서 **80**, hello 다음 작업을 구성 해야 합니다.

1. 포트 80에서 수신 대기하는 서비스를 작성합니다. Hello 서비스 ServiceManifest.xml에서 포트 80을 구성 하 고 hello 서비스, 예를 들어 자체 호스트 된 웹 서버에서에서 수신기를 엽니다.

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. Azure에서 서비스 패브릭 클러스터를 만들고 포트 지정 **80** hello 서비스를 호스팅할 hello 노드 형식에 대 한 사용자 지정 끝점 포트로 합니다. 설정할 수 노드 유형을 여러 개 있는 경우는 *배치 제약 조건* 에 hello 서비스 tooensure hello 사용자 지정 끝점 포트를 열어야 있는 hello 노드 형식에만 실행 합니다.

    ![노드 형식에서 포트 열기][4]
3. Hello 클러스터를 만든 후에 포트 80에서 hello 클러스터 리소스 그룹 tooforward 트래픽 hello Azure 부하 분산 장치를 구성 합니다. Hello Azure 포털을 통해 클러스터를 만들 때이 설정은 자동으로 구성 된 각 사용자 지정 끝점 포트에 대 한 합니다.

    ![Hello Azure 부하 분산 장치에서에서 트래픽을 전달합니다][5]
4. 사용 하 여 Azure 부하 분산 장치 프로브 toodetermine 여부 hello 또는 하지 toosend 트래픽 tooa 특정 노드. hello는 주기적으로 검사 끝점을 검색이 각 노드 toodetermine hello 노드 응답 여부에 있습니다. Hello 검색이 실패 한 후 구성 된 횟수 만큼 tooreceive 응답 하면 전송 트래픽 toothat 노드의 hello 부하 분산 장치를 중지 합니다. Hello Azure 포털을 통해 클러스터를 만들 때는 프로브는 자동으로 설정 구성 된 각 사용자 지정 끝점 포트에 대 한 합니다.

    ![Hello Azure 부하 분산 장치에서에서 트래픽을 전달합니다][8]

Hello Azure 부하 분산 장치 및 hello 프로브만 hello에 대 한 알 수 있는 중요 한 tooremember는 *노드*, 하지 hello *서비스* hello 노드에서 실행 합니다. hello Azure 부하 분산 장치는 항상 toohello 프로브 응답 하는 트래픽을 toonodes 송신할 tooensure 서비스는 hello 노드 수 toorespond toohello 프로브를 사용할 수 주의 해야 합니다.

## <a name="reliable-services-built-in-communication-api-options"></a>Reliable Services: 기본 제공 통신 API 옵션
hello 신뢰할 수 있는 서비스 프레임 워크는 몇 가지 미리 작성 된 통신 옵션 포함 되어 있습니다. hello 의사 결정에 대 한 하나 가장 적합 한 사용자의 프로그래밍 모델, hello 통신 프레임 워크 및 프로그래밍 언어 서비스 작성 된 hello hello hello 선택에 따라 달라 집니다.

* **특정 프로토콜이 없습니다:** 통신 프레임 워크의 특정 항목을 선택한 없는 하지만 원하는 tooget 켜져 있고 실행 중인 어떤 신속 하 게 경우 hello 이상적인 옵션을는 [원격 서비스](service-fabric-reliable-services-communication-remoting.md)를 허용 하는 신뢰할 수 있는 서비스 및 Reliable Actors에 대 한 강력한 형식의 원격 프로시저를 호출합니다. 이 가장 쉬운 hello 및 가장 빠른 방법은 tooget 서비스 통신을 시작 합니다. 서비스 원격은 서비스 주소, 연결, 다시 시도 및 오류 처리의 확인을 처리합니다. 이 기능은 C# 및 Java 응용 프로그램에 둘 다 사용할 수 있습니다.
* **HTTP**: 언어 중립적 통신의 경우, HTTP는 Service Fabric에서 전적으로 지원하는 다양한 언어로 사용할 수 있는 도구 및 HTTP 서버와 함께 업계 표준 선택을 제공합니다. 서비스는 C# 응용 프로그램용 [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md)를 포함하여 사용 가능한 모든 HTTP 스택을 사용할 수 있습니다. C#으로 작성 하는 클라이언트 hello를 활용할 수 `ICommunicationClient` 및 `ServicePartitionClient` 반면 클래스 Java에 대 한 hello를 사용 하 여 `CommunicationClient` 및 `FabricServicePartitionClient` 클래스, [서비스 확인, HTTP 연결 및 다시 시도 루프에 대 한](service-fabric-reliable-services-communication.md)합니다.
* **WCF**: 프로그램 통신 프레임 워크와 WCF를 사용 하는 기존 코드를 있는 경우 hello를 사용할 수 있습니다 `WcfCommunicationListener` hello 서버 측에 대 한 및 `WcfCommunicationClient` 및 `ServicePartitionClient` hello 클라이언트에 대 한 클래스입니다. 그러나 이 기능은 Windows 기반 클러스터의 C# 응용프로그램에만 사용할 수 있습니다. 자세한 내용은이 문서에 대 한 참조 [hello 통신 스택의 WCF 기반 구현](service-fabric-reliable-services-communication-wcf.md)합니다.

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>사용자 지정 프로토콜 및 기타 통신 프레임워크 사용
서비스는 TCP 소켓을 통한 사용자 지정 이진 프로토콜이든 [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 또는 [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/)를 통한 스트리밍 이벤트이든 통신에 대한 모든 프로토콜 또는 프레임워크를 사용할 수 있습니다. 서비스 패브릭에서 추출 하는 통신 모든 hello toodiscover 작업과 연결 하는 동안 통신 스택을를 연결할 수 있는 Api를 제공 합니다. Hello에 대 한이 문서를 참조 [신뢰할 수 있는 서비스 통신 모델](service-fabric-reliable-services-communication.md) 내용을 확인 합니다.

## <a name="next-steps"></a>다음 단계
Hello 개념 및 hello에서 사용할 수 있는 Api에 대 한 자세한 정보에 대해 알아봅니다 [신뢰할 수 있는 서비스 통신 모델](service-fabric-reliable-services-communication.md), 다음 시작 신속 하 게 [원격 서비스](service-fabric-reliable-services-communication-remoting.md) 심층 분석 toolearn 어떻게 이동 또는 toowrite는 통신 수신기를 사용 하 여 [자체 호스트 하는 OWIN과 웹 API](service-fabric-reliable-services-communication-webapi.md)합니다.

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
