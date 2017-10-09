---
title: "연결 된 Azure IoT Suite aaaDeploy 팩터리 게이트웨이 | Microsoft Docs"
description: "Windows 또는 Linux tooenable 연결 toohello에 게이트웨이 toodeploy 팩터리를 연결 하는 방법을 미리 솔루션을 구성 합니다."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>연결 된 hello 팩터리 미리 구성 된 솔루션에 대 한 Windows 또는 Linux에서 게이트웨이 배포

hello 소프트웨어 필수 toodeploy hello 연결 된 팩터리 미리 구성 된 솔루션에 대 한 게이트웨이 a의 두 구성 요소:

* hello *OPC 프록시* 연결 tooIoT 허브를 설정 합니다. hello *OPC 프록시* hello에서 명령 및 제어 메시지에 대 한 대기 hello 연결 된 팩터리 솔루션 포털에서 실행 되는 OPC 브라우저를 통합 하는 다음 합니다.
* hello *OPC 게시자* tooexisting 온-프레미스 OPC UA 서버를 연결 하 고 tooIoT 허브에서 원격 분석 메시지를 전달 합니다.

두 구성 요소는 오픈 소스이며 GitHub의 원본 및 Docker 컨테이너로 사용할 수 있습니다.

| GitHub | DockerHub |
| ------ | --------- |
| [OPC 게시자][lnk-publisher-github] | [OPC 게시자][lnk-publisher-docker] |
| [OPC 프록시][lnk-proxy-github] | [OPC 프록시][lnk-proxy-docker] |

없음 공용 IP 주소 또는 구멍 hello 게이트웨이 방화벽에서는 어느 구성 요소에 필요 합니다. OPC 프록시 hello 및 OPC 게시자 443, 5671, 및 8883 아웃 바운드 포트만 사용합니다.

hello이 문서의 단계 방법을 보여 줍니다 게이트웨이 중 하나에서 Docker를 사용 하 여 a toodeploy [Windows](#windows-deployment) 또는 [Linux](#linux-deployment)합니다. hello 게이트웨이 연결 toohello 연결 팩터리 미리 구성 된 솔루션을 수 있습니다.

> [!NOTE]
> hello 게이트웨이 소프트웨어 hello Docker 컨테이너에서 실행 되는 [Azure IoT 가장자리]합니다.

## <a name="windows-deployment"></a>Windows 배포

> [!NOTE]
> 게이트웨이 장치가 아직 없는 경우 파트너로부터 상용 게이트웨이를 구입하는 것이 좋습니다. Hello 방문 [Azure IoT 장치 카탈로그] hello와 호환 되는 게이트웨이 장치 목록은 대 한 팩터리 솔루션을 연결 합니다. Hello 게이트웨이 설치 하는 hello 장치 tooset 함께 제공 되는 hello 지침을 따릅니다. 또는 기존 게이트웨이 중 하나를 설정 하는 지침 toomanually 다음 hello를 사용 합니다.

### <a name="install-docker"></a>Docker 설치

Windows 기반 게이트웨이 장치에 [Windows용 Docker]를 설치합니다. Windows Docker 설치 중에 Docker가 있는 호스트 컴퓨터 tooshare 사용자 드라이브를 선택 합니다. 다음 스크린 샷에 표시 하면 Windows 시스템에서 D hello 드라이브를 공유 하는 hello:

![Docker 설치][img-install-docker]

라는 폴더를 만든 다음 **docker** hello의 hello 루트에서 드라이브를 공유 합니다.
Hello에서 docker를 설치한 후이 단계를 수행할 수도 있습니다 **설정을** 메뉴.

### <a name="configure-hello-gateway"></a>Hello 게이트웨이 구성

1. Hello 필요한 **iothubowner** Azure IoT Suite의 연결 문자열 연결 팩터리 배포 toocomplete hello 게이트웨이 배포 합니다. Hello에 [Azure 포털], IoT Hub hello 리소스 그룹에 연결 하는 hello 팩터리 솔루션을 배포할 때 만든 tooyour 이동 합니다. 클릭 **공유 액세스 정책을** tooaccess hello **iothubowner** 연결 문자열:

    ![Hello IoT 허브 연결 문자열][img-hub-connection]

    복사 hello **연결 문자열이 며 기본 키** 값입니다.

1. Hello 두 게이트웨이 모듈을 실행 하 여 IoT 허브에 대 한 hello 게이트웨이 구성 **면** 으로 명령 프롬프트에서:

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  hello 형태로 표시 hello 이름 toogive tooyour OPC UA 게시자는 **게시자.&lt; 정규화 된 도메인 이름&gt;**합니다. 예를 들어, 출하 시 네트워크를 호출 하면 **myfactorynetwork.com**, hello **ApplicationName** 값은 **publisher.myfactorynetwork.com**합니다.
    * **&lt;IoTHubOwnerConnectionString&gt;**  는 hello **iothubowner** hello 이전 단계에서 복사한 연결 문자열입니다. 이 연결 문자열은이 단계에만 사용, 단계를 수행 하는 hello에 필요 하지 않습니다.

    사용 하면 hello d: 매핑된\\docker 폴더 (hello `-v` 인수) 이후 toopersist hello hello 게이트웨이 모듈을 사용 하는 두 X.509 인증서입니다.

### <a name="run-hello-gateway"></a>Hello 게이트웨이 실행 합니다.

1. 다음 명령을 hello를 사용 하 여 hello 게이트웨이 다시 시작 합니다.

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. 보안상의 이유로 hello 두 X.509 인증서 hello d:에에서 유지\\docker 폴더 hello 개인 키를 포함 합니다. Toothis 폴더 toohello 자격 증명 액세스 제한 (일반적으로 **관리자**) toorun hello Docker 컨테이너를 사용 합니다. 마우스 오른쪽 단추로 클릭 hello d:\\docker 폴더 선택 **속성**, 다음 **보안**, 차례로 **편집**합니다. **Administrators**에 모든 권한을 제공하고 다른 모든 사용자를 제거합니다.

    ![Grant 권한 tooDocker 공유][img-docker-share]

1. 네트워크 연결을 확인합니다. 명령 프롬프트에서 명령을 실행 hello `ping publisher.<your fully qualified domain name>` tooping 게이트웨이 합니다. Hello 대상에 연결할 수 없는 경우에 hello IP 주소 및 게이트웨이에 게이트웨이 toohello 호스트 파일의 이름을 추가 합니다. hello 호스트 파일은 hello **Windows\\System32\\드라이버\\등** 폴더입니다.

1. Hello 게이트웨이가 실행 되는 로컬 OPC UA 클라이언트를 사용 하 여 tooconnect toohello 게시자를 다음을 시도 합니다. OPC UA 끝점 URL이 hello `opc.tcp://publisher.<your fully qualified domain name>:62222`합니다. OPC UA 클라이언트가 없으면 [오픈 소스 OPC UA 클라이언트]를 다운로드하여 사용할 수 있습니다.

1. 로컬 테스트를 성공적으로 완료 되 면 탐색할 toohello **OPC UA 서버 연결** hello 연결 된 팩터리 솔루션 포털의 페이지입니다. Hello 게시자 끝점 URL을 입력 (`tcp://publisher.<your fully qualified domain name>:62222`)를 클릭 하 고 **연결**합니다. 인증서 경고가 표시되면 **계속**을 클릭합니다. 다음 오류가 발생 하는 hello 게시자 hello UA 웹 클라이언트를 신뢰 하지 않습니다. tooresolve이 오류를 복사 hello **UA 웹 클라이언트** hello에서 인증서를 **d:\\docker\\거부 인증서\\인증서** 폴더 toohello **D:\\docker\\UA 응용 프로그램\\인증서** hello 게이트웨이에서 폴더입니다. Hello 게이트웨이의 toorestart가 필요가 없습니다. 이 단계를 반복합니다. Hello 클라우드에서 이제 toohello 게이트웨이 연결할 수 있으며, 준비 tooadd OPC UA 서버 toohello 솔루션 됩니다.

### <a name="add-your-opc-ua-servers"></a>OPC UA 서버 추가

1. Toohello 찾아보기 **OPC UA 서버 연결** hello 연결 된 팩터리 솔루션 포털의 페이지입니다. Hello 연결 된 팩터리 포털 hello 및 OPC UA 서버 hello 간 트러스트 섹션 tooestablish 앞 hello와 같은 단계를 따릅니다. 이 단계를 설정 hello에서 hello 인증서의 상호 신뢰 팩터리 포털 및 hello OPC UA 서버를 연결 하 고 연결을 만듭니다.

1. OPC UA 노드 트리 OPC UA 서버 hello 찾아보기 hello OPC 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다. 게시 toowork 이러한 방식으로에 대 한 OPC UA 서버 hello 및 hello 게시자는 hello에 있어야 합니다. 동일한 네트워크입니다. 즉, hello 정규화 된 도메인 이름이 hello 게시자의 이름 인지 **publisher.mydomain.com** 의 예를 들어 OPC UA 서버 수 있어야 하는 hello hello 정규화 된 도메인 이름을 차례로 **myopcuaserver.mydomain.com**. 다른 설치 프로그램의 경우 노드 toohello publishesnodes.json 파일 hello에 수동으로 추가할 수 있습니다 **d:\\docker** 폴더입니다. hello publishesnodes.json 파일 생성 hello에 처음 성공 OPC 노드의 게시 합니다.

1. 원격 분석 hello 게이트웨이 장치에서 이제 이동합니다. Hello에 hello 원격 분석을 볼 수 있습니다 **공장 위치** hello 연결 된 팩터리 포털의 보기 **새 팩터리**합니다.

## <a name="linux-deployment"></a>Linux 배포

> [!NOTE]
> 게이트웨이 장치가 아직 없는 경우 파트너로부터 상용 게이트웨이를 구입하는 것이 좋습니다. Hello 방문 [Azure IoT 장치 카탈로그] hello와 호환 되는 게이트웨이 장치 목록은 대 한 팩터리 솔루션을 연결 합니다. Hello 게이트웨이 설치 하는 hello 장치 tooset 함께 제공 되는 hello 지침을 따릅니다. 또는 기존 게이트웨이 중 하나를 설정 하는 지침 toomanually 다음 hello를 사용 합니다.

Linux 게이트웨이 장치에서 [Docker를 설치]합니다.

### <a name="configure-hello-gateway"></a>Hello 게이트웨이 구성

1. Hello 필요한 **iothubowner** Azure IoT Suite의 연결 문자열 연결 팩터리 배포 toocomplete hello 게이트웨이 배포 합니다. Hello에 [Azure 포털], IoT Hub hello 리소스 그룹에 연결 하는 hello 팩터리 솔루션을 배포할 때 만든 tooyour 이동 합니다. 클릭 **공유 액세스 정책을** tooaccess hello **iothubowner** 연결 문자열:

    ![Hello IoT 허브 연결 문자열][img-hub-connection]

    복사 hello **연결 문자열이 며 기본 키** 값입니다.

1. Hello 두 게이트웨이 모듈을 실행 하 여 IoT 허브에 대 한 hello 게이트웨이 구성 **면** 로 셸을에서:

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  OPC UA 응용 프로그램 hello 게이트웨이 hello 형식으로 생성 하는 hello의 hello 이름인 **게시자.&lt; 정규화 된 도메인 이름&gt;**합니다. 예를 들면 **publisher.microsoft.com**과 같습니다.
    * **&lt;IoTHubOwnerConnectionString&gt;**  는 hello **iothubowner** hello 이전 단계에서 복사한 연결 문자열입니다. 이 연결 문자열은이 단계에만 사용, 단계를 수행 하는 hello에 필요 하지 않습니다.

    Hello를 사용 하 여 **공유 /** 폴더 (hello `-v` 인수) 이후 toopersist hello hello 게이트웨이 모듈을 사용 하는 두 X.509 인증서입니다.

### <a name="run-hello-gateway"></a>Hello 게이트웨이 실행 합니다.

1. 다음 명령을 hello를 사용 하 여 hello 게이트웨이 다시 시작 합니다.

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. 보안상의 이유로 hello 두 X.509 인증서 hello에 유지 **공유 /** 폴더 hello 개인 키를 포함 합니다. 제한 toothis 폴더 toohello 자격 증명 액세스 toorun를 사용 하 여 hello Docker 컨테이너입니다. 에 대 한 tooset hello 권한을 **루트** 만 hello를 사용 하 여 `chmod` 셸 hello 폴더에 명령 합니다.

1. 네트워크 연결을 확인합니다. Hello 명령을 입력 하는 셸에서 `ping publisher.<your fully qualified domain name>` tooping 게이트웨이 합니다. Hello 대상에 연결할 수 없는 경우에 hello IP 주소 및 게이트웨이에 게이트웨이 tooyour 호스트 파일의 이름을 추가 합니다. hello 호스트 파일은 hello **/등** 폴더입니다.

1. Hello 게이트웨이가 실행 되는 로컬 OPC UA 클라이언트를 사용 하 여 tooconnect toohello 게시자를 다음을 시도 합니다. OPC UA 끝점 URL이 hello `opc.tcp://publisher.<your fully qualified domain name>:62222`합니다. OPC UA 클라이언트가 없으면 [오픈 소스 OPC UA 클라이언트]를 다운로드하여 사용할 수 있습니다.

1. 로컬 테스트를 성공적으로 완료 되 면 탐색할 toohello **OPC UA 서버 연결** hello 연결 된 팩터리 솔루션 포털의 페이지입니다. Hello 게시자 끝점 URL을 입력 (`tcp://publisher.<your fully qualified domain name>:62222`)를 클릭 하 고 **연결**합니다. 인증서 경고가 표시되면 **계속**을 클릭합니다. 다음 오류가 발생 하는 hello 게시자 hello UA 웹 클라이언트를 신뢰 하지 않습니다. tooresolve이 오류를 복사 hello **UA 웹 클라이언트** hello에서 인증서를 **/공유/인증서/인증 거부 됨** 폴더 toohello **/shared/UA 응용 프로그램/인증서** hello 게이트웨이 폴더입니다. Hello 게이트웨이의 toorestart가 필요가 없습니다. 이 단계를 반복합니다. Hello 클라우드에서 이제 toohello 게이트웨이 연결할 수 있으며, 준비 tooadd OPC UA 서버 toohello 솔루션 됩니다.

### <a name="add-your-opc-ua-servers"></a>OPC UA 서버 추가

1. Toohello 찾아보기 **OPC UA 서버 연결** hello 연결 된 팩터리 솔루션 포털의 페이지입니다. Hello 연결 된 팩터리 포털 hello 및 OPC UA 서버 hello 간 트러스트 섹션 tooestablish 앞 hello와 같은 단계를 따릅니다. 이 단계를 설정 hello에서 hello 인증서의 상호 신뢰 팩터리 포털 및 hello OPC UA 서버를 연결 하 고 연결을 만듭니다.

1. OPC UA 노드 트리 OPC UA 서버 hello 찾아보기 hello OPC 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다. 게시 toowork 이러한 방식으로에 대 한 OPC UA 서버 hello 및 hello 게시자는 hello에 있어야 합니다. 동일한 네트워크입니다. 즉, hello 정규화 된 도메인 이름이 hello 게시자의 이름 인지 **publisher.mydomain.com** 의 예를 들어 OPC UA 서버 수 있어야 하는 hello hello 정규화 된 도메인 이름을 차례로 **myopcuaserver.mydomain.com**. 다른 설치 프로그램의 경우 노드 toohello publishesnodes.json 파일 hello에 수동으로 추가할 수 있습니다 **공유 /** 폴더입니다. hello publishesnodes.json 자동으로 생성 hello에 처음 성공 OPC 노드의 게시 합니다.

1. 원격 분석 hello 게이트웨이 장치에서 이제 이동합니다. Hello에 hello 원격 분석을 볼 수 있습니다 **공장 위치** hello 연결 된 팩터리 포털의 보기 **새 팩터리**합니다.

## <a name="next-steps"></a>다음 단계

hello 연결 된 팩터리의 hello 아키텍처에 대해 자세히 toolearn 미리 솔루션을 구성을 참조 하십시오. [솔루션 연습을 미리 구성 된 연결 된 팩터리][lnk-walkthrough]합니다.

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Windows용 Docker]: https://www.docker.com/docker-windows
[Azure IoT 장치 카탈로그]: https://catalog.azureiotsuite.com/?q=opc
[Azure 포털]: http://portal.azure.com/
[오픈 소스 OPC UA 클라이언트]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[Docker를 설치]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT 가장자리]: https://github.com/Azure/iot-edge

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy