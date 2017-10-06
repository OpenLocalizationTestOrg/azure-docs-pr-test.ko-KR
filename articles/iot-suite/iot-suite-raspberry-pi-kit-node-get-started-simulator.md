---
title: "aaaConnect 라스베리 Pi tooAzure IoT Suite 된 시뮬레이션 된 원격 분석 Node.js를 사용 하 여 | Microsoft Docs"
description: "Hello 라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트 hello와, Azure IoT Suite를 사용 합니다. Node.js tooconnect 프로그램 라스베리 Pi toohello 원격 모니터링 솔루션을 사용 하 고 시뮬레이트된 원격 분석 toohello 클라우드 보내고 toomethods hello 솔루션 대시보드에서 호출 알림에 응답 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a>원격 모니터링 솔루션 라스베리 Pi 3 toohello 사용자를 연결 하 고 Node.js를 사용 하 여 시뮬레이션 된 원격 분석

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

이 자습서에서는 toouse hello 라스베리 Pi 3 toosimulate 온도 및 습도 데이터 toosend toohello의 클라우드를 보여 줍니다. hello 자습서를 사용합니다.

- Raspbian OS 프로그래밍 언어를 Node.js hello 및 Node.js tooimplement 샘플 장치에 대 한 Microsoft Azure IoT SDK hello 합니다.
- hello IoT Suite 원격 모니터링 솔루션 hello 클라우드 기반 백 엔드 응용 프로그램으로 미리 구성 합니다.

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> 원격 hello 솔루션 프로 비전 한 일련의 Azure 구독에서 Azure 서비스를 모니터링합니다. hello 배포 실제 엔터프라이즈 아키텍처를 반영합니다. 종료 되었음을 tooavoid 불필요 한 Azure 사용료가 부과 azureiotsuite.com에 hello 미리 구성 된 솔루션의 인스턴스를 삭제 합니다. 미리 구성 된 솔루션을 다시 hello 필요, 있습니다 쉽게 다시 만들 수 있습니다. Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a>다운로드 하 고 hello 샘플 구성

이제 다운로드 하 고 라스베리 원주율 hello 원격 모니터링 클라이언트 응용 프로그램을 구성할 수 있습니다.

### <a name="install-nodejs"></a>Node.js 설치

아직 그렇게 하지 않은 경우 Raspberry Pi에 Node.js를 설치합니다. Node.js 용 IoT SDK hello 0.11.5 이상 버전의 Node.js 필요합니다. hello 다음 단계 방법을 보여 줍니다 라스베리 원주율 tooinstall Node.js v6.10.2:

1. 다음 명령은 tooupdate hello 라스베리 Pi를 사용 합니다.

    ```sh
    sudo apt-get update
    ```

1. 다음 명령은 toodownload hello Node.js 바이너리 tooyour 라스베리 Pi hello를 사용 합니다.

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. 사용 하 여 hello 다음 명령 tooinstall hello 이진 파일을 사용할 수 있습니다.

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Node.js v6.10.2를 성공적으로 설치한 명령 tooverify 다음 hello를 사용 합니다.

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a>Hello 리포지토리 복제

아직 이미 하지 않은 경우 복제 hello 나오는 프로그램 Pi에 따라 종료에서 명령을 실행 하 여 저장소 hello 필요 합니다.

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Hello 장치 연결 문자열 업데이트

Hello open hello 샘플 소스 파일 **nano** hello 다음 명령을 사용 하 여 편집기:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

Hello 줄을 찾습니다.

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Hello 장치와 IoT 허브 정보를 만들고이 자습서의 시작 부분 hello에 저장 된 hello 자리 표시자 값을 바꿉니다. 변경 내용을 저장 (**Ctrl-O**, **Enter**) 및 exit hello 편집기 (**Ctrl-X**).

## <a name="run-hello-sample"></a>Hello 예제 실행

실행된 hello 다음 tooinstall hello hello 샘플에 대 한 필수 구성 요소 패키지가 명령:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

이제 라스베리 Pi hello에 hello 샘플 프로그램을 실행할 수 있습니다. Hello 명령을 입력 합니다.

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

hello 다음 샘플 출력은 hello 라스베리 Pi hello 명령 프롬프트에서 참조 하는 hello 출력 예입니다.

![Raspberry Pi 앱의 출력][img-raspberry-output]

키를 눌러 **Ctrl-c** 언제 든 지 tooexit hello 프로그램입니다.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a>다음 단계

Hello 방문 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/) 에 더 많은 샘플 및 Azure IoT에 대 한 설명서입니다.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
